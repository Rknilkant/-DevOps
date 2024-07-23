# Add Multiple SSH keys to an EC2 Server


SSH keys are a way to authenticate yourself to a remote server. They are a more secure way to authenticate yourself to a remote server than using a password. SSH keys are a pair of keys, a public key and a private key. The public key is stored on the remote server and the private key is stored on your local machine. When you try to authenticate yourself to the remote server, the remote server will check if the public key matches the private key. If it does, you are authenticated.

EC2 instances are virtual machines that you can spin up on AWS and deploy your application on. AWS only allows you to create and attach a single SSH key to an EC2 instance. However, you may want to have multiple SSH keys attached to an EC2 instance. Some examples of when you may want to do this are:

- You have multiple developers working on the same project and you want to give them access to the EC2 instance.
- You are using a CI/CD tool like Jenkins and you want to give it access to the EC2 instance.
- You want to give access to some other service that needs to access the EC2 instance.
Sharing your personal SSH key is not a good idea because you might be using the same key for multiple different services. If the key is compromised, then all of your services are compromised. So, it is a good idea to create a new SSH key for each service that you want to give access to.

In this guide, we will see how to create and add multiple SSH keys to an EC2 instance.

## Step 1: Create a new SSH key
To create a new SSH key, you can use the ssh-keygen command. The ssh-keygen command is a tool for creating new authentication keys. It is available on most Linux distributions and macOS. You can use the following command to create a new SSH key:

```ssh-keygen -t rsa -b 4096 -f ./key_name  ```

The -t flag specifies the type of key to create. The -b flag specifies the number of bits in the key to create. The -f flag specifies the file in which to save the key. The command above will create a new SSH key with 4096 bits and save it in a file called key_name.

The command above will create two files, key_name and key_name.pub. The key_name file is the private key and the key_name.pub file is the public key.

Private key
The private key is the key that you will use to authenticate yourself to the remote server. You should keep this key safe and not share it with anyone. If someone gets access to your private key, they can impersonate you on the remote server.

Public key
The public key is the key that you will give to the remote server. The remote server will use this key to authenticate you. You can share this key with anyone.

## Step 2: Allow access to the Key
There are two ways to add the SSH key to the remote EC2 instance. You can either use the ssh-copy-id command or you can manually add the key to the authorized_keys file.

### Option 1: Using the ssh-copy-id
The ssh-copy-id command is a tool for copying SSH keys to a remote server. You can use the following command to copy the SSH key to the remote server:

```ssh-copy-id -i ./key_name.pub user@remote_server``` 

The -i flag specifies the file that contains the public key. The user is the username of the user on the remote server. The remote_server is the IP address or domain name of the remote server.

### Option 2: Manually add the Key
You can also manually add the key to the authorized_keys file. The authorized_keys file is a file that contains all the public keys that are allowed to authenticate to the remote server.

First of all, you need to copy the content of the public key file to your clipboard. Next, connect to the remote server using SSH. You can use the following command to connect to the remote server:

```ssh user@remote_server```


The user is the username of the user on the remote server. The remote_server is the IP address or domain name of the remote server. Once you are connected to the remote server, open the authorized_keys file using the following command:

```sudo vi ~/.ssh/authorized_keys```

Once you are in the authorized_keys file, press the i key to enter insert mode. Paste the content of the public key file to the end of the file. Once you are done, press the esc key to exit insert mode. Then, type :wq and press enter to save the file.

## Step 3: Test the SSH key
Once you have copied the public key to the remote server, you can test the SSH key on your local machine. You can use the following command to test the SSH key:

```ssh -i ./key_name user@remote_server```

The -i flag specifies the file that contains the private key. The user is the username of the user on the remote server. The remote_server is the IP address or domain name of the remote server.

If everything is set up correctly, you should be able to connect to the remote server using the SSH key.
