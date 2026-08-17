# Simplifying SSH Access to Sherlock and OAK

If you regularly connect to Stanford systems such as Sherlock or OAK, it is worth setting up an SSH configuration file. This provides two major benefits:

1. Connect using a short alias (e.g., `ssh sherlock`) instead of typing the full hostname and username each time.
2. Reuse an existing authenticated connection across multiple terminals, `scp`, `rsync`, and VS Code sessions, reducing repeated Duo prompts.

## Step 1: Create an SSH Configuration File

On your local computer (not on Sherlock or OAK), open a terminal and run:

```bash
mkdir -p ~/.ssh
touch ~/.ssh/config
chmod 600 ~/.ssh/config
```

Open the configuration file:

```bash
nano ~/.ssh/config
```

## Step 2: Add a Sherlock Host Definition

Replace `SUNETID` with your Stanford username and add the following to the file:

```text
Host sherlock
    HostName login.sherlock.stanford.edu
    User SUNETID

    ControlMaster auto
    ControlPersist 2h
    ControlPath ~/.ssh/%C
```

### Saving and Exiting Nano

If you are using the `nano` editor:

1. Press **Ctrl+O** ("Write Out") to save the file.
2. Press **Enter** to confirm the filename.
3. Press **Ctrl+X** to exit nano.

## Step 3: Test the Configuration

Connect to Sherlock:

```bash
ssh sherlock
```

You should now be able to connect using the short alias `sherlock`.

## Step 4: Verify Connection Reuse

Open a first terminal and connect:

```bash
ssh sherlock
```

Complete Duo authentication as usual.

Then open a second terminal window and run:

```bash
ssh sherlock
```

If configured correctly, the second connection should open immediately using the existing authenticated session.

This also works for commands such as:

```bash
scp file.txt sherlock:~
rsync -av data/ sherlock:~/project/
```

and often for VS Code Remote SSH connections.

## Using OAK Instead

The same approach can be used for OAK. Add a separate host definition:

```text
Host oak
    HostName oak.stanford.edu
    User SUNETID

    ControlMaster auto
    ControlPersist 2h
    ControlPath ~/.ssh/%C
```

After saving, connect using:

```bash
ssh oak
```

## Useful Commands

Check whether a shared connection currently exists:

```bash
ssh -O check sherlock
```

Close the shared connection manually:

```bash
ssh -O exit sherlock
```

Replace `sherlock` with `oak` when working with OAK.

## Optional Settings for Advanced Users

Some Stanford users may benefit from additional SSH options:

```text
GSSAPIAuthentication yes
GSSAPIDelegateCredentials yes
```

These settings can simplify workflows that rely on Stanford Kerberos credentials and authentication to downstream Stanford services.

Users who run graphical Linux applications over SSH may also find the following useful:

```text
ForwardX11Trusted yes
```

Most users working through the command line, VS Code Remote SSH, Jupyter, or web interfaces will not need this setting.

## Notes

* The SSH configuration file lives on your local machine, not on Sherlock or OAK.
* Sherlock and OAK maintain separate shared connections.
* The first connection still requires normal authentication and Duo approval.
* Connection reuse does not bypass security requirements; it simply allows subsequent connections to reuse an already-authenticated session.
* The same host aliases can be used by command-line tools such as `scp`, `sftp`, `rsync`, and many IDEs that support SSH connections.
