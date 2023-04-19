# Commands
Check for updates that are available for the operating system and installed packages.

```
    1  sudo apt update 
```

Check if Java is installed.
```
    2  java --version 
```

By default, it is not installed so you will get the following message:

```
	-bash: java: command not found
```

Install JRE.
```
    3  sudo apt install default-jre 
```

It will list the packages to be installed, and print the following prompt

```

	After this operation, 373 MB of additional disk space will be used.
	Do you want to continue? [Y/n]

```

type `y` and hit `Enter`


Now, let's check again if Java Runtime Environment is insalled. 
```
    4  java --version 
```

If step 3 was successful, you should get a message similar to the following:

```
	openjdk 11.0.16 2022-07-19
	OpenJDK Runtime Environment (build 11.0.16+8-post-Debian-1deb11u1)
	OpenJDK 64-Bit Server VM (build 11.0.16+8-post-Debian-1deb11u1, mixed mode, sharing)

```
Note that version numbers can be different, which is fine


Check if `git` is installed.
```
    5  git 
```

Again, you get a message that this command is not found, because git is not installed yet. Let's Install it.
```
    6  sudo apt install git 
```

Check version of your git installation.
```
    7  git --version 
```

Configure git.
```
    8  git config --global user.name "Your Name" 
```

```
    9  git config --global user.email "Your-Email-Name@ou.edu" 
```

Clone your repository from `GitHub`.
If you have two-factor authentication enabled on your account, you will need to create a [personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) and enter it instead of your password.
```
   10  git clone "Lab10 GitHub URL"
```

Check if you see the new directory listed with your repo in it.
```
   11  ls 
```

Change directory to your project.
```
   12  cd lab10-github-username/ 
```

```
   13  ls 
```

```
   14  cd src 
```

```
   15  ls 
```

```
   16  cd html 
```

```
   17  ls 
```

Compile your Java program.
```
   18  javac MakePage.java 
```

We did not install JDK, and so, we cannot compile just yet. More packages to install.
```
   19  ls
```

Install the JDK.
```
   20  sudo apt install default-jdk 
```

Check version of your freshly installed JDK.
```
   21  javac --version 
```

```
   22  ls 
```

Complie your Java program.
```
   23  javac MakePage.java 
```

```
   24  ls 
```

If compilation was successful, you should see a new file was created: `MakePage.class`

Try to run your java program.
```
   25  java MakePage 
```

You should get the following error:

```

	Error: Could not find or load main class MakePage
	Caused by: java.lang.NoClassDefFoundError: html/MakePage (wrong name: MakePage)

```
This is because you need the full class name, including the package name (html).
To do this, you need to go up one level in the directory hierarchy by executing
```
   26	cd ..
	
```

Then now run using the full qualified name as follows:
```
   27 java html/MakePage
```

Now, you'll get a different error, raised by a `java.io.FileNotFoundException`. To understand 
why you get this error, look at the source code and you'll find that it expects a directory called
`colors` in the current directory to write the files to. Since this directory does not exist, we get
the exception. 

To fix this error, simply make the `colors` directory in the current directory by executing:

```
   28	mkdir colors

```

Now, try to run the program again

```
   29 java html/MakePage
```

You should get rid of that error now!

Check if you have `nano` installed.
```
   30  nano 
```

If you get a `command not found` message, install `nano`, which is a text editor that we will use later to edit our java program and a  configuration file.
```
   31  sudo apt install nano 
```

Now, we have to install `nginx`, the webserver application we will use.
```
   32  sudo apt install nginx 
```

In the list of VM instances on the GCP website (the same page where you clicked the link to connect via SSH), there is a column labeled "External IP."
Copy the external IP address of your instance, and try to connect to it in a browser.
The URL of your server is "http://" + ip-address.
For instance, if the IP address is 1.2.3.4, the URL is "http://1.2.3.4".
(You can click the IP address on the GCP website to connect, but you'll need to change the prefix from "https" to "http".). If you have allowed http and https traffic 
while creating the VM instance, you should be able to see the "Welcome to nginx" page in your browser.


Now, go to the directory that will hold your web pages. `pushd` is more versatile than `cd`. You can `pushd` to the directory of your choice, and `popd` will take you back to the previous directory.
```
   33  pushd /var/www/html 
```

```
   34  ls 
```

Create a directory for your pages.
```
   35  mkdir colors 
```

You'll get a `Permission denied` error after executing this command, because this is considered a system directory.

You may have to be a `super users` to do it.
```
   36  sudo mkdir colors 
```

Change the ownership of the directory and its content.
```
   37  sudo chown -R $USER:$USER /var/www/html/colors 
```

Change the access permissions to the above mentioned directory.
```
   38  sudo chmod -R 755 /var/www/html/colors 
```

Check if you can access the directory.
```
   39  curl localhost/colors 
```

```
   40  curl localhost/ 
```

Now, we have to modify the configuration of your `nginx` installation, to allow for directory listing of `colors`.
```
   41  pushd /etc/nginx/sites-enabled/ 
```

```
   42  ls 
```

```
   43  sudo nano default 
```

You have to change the default settings for your web server.
You have to allow for the directory content to be listed. 
Add the following below the entry `location / { try_files $uri $uri/ =404; }`:
```
        location /colors {
                autoindex on;
        }
```

```
   44  sudo nginx -t 
```

After the config file modification, we have to restart our `nginx` installation.
```
   45  sudo systemctl restart nginx 
```

Verify that you can see the `colors` directory in your browser by opening the URL "http://" + external-ip + "/colors".

```
   46  popd 
```

```
   47  ls 
```

```
   48  cd colors 
```

```
   49  pwd 
```

If you followed the instructions closely, this should print

```
	/var/www/html/colors

```


```
   50  popd 
```

```
   51  ls 
```

this brings us back to the `src` directory of our java project


```
   52  cd html 
```

```
   53  ls 
```

Open the source file for the program in nano:
```
   54  nano MakePage.java 
```

Make the following changes:

Switch the value of the constant `DIRECTORY` from `"./colors/"` to `"/var/www/html/colors/"`.
Save (write out) and exit.

Recompile the code:
```
   55  javac MakePage.java
```

```
   56  cd .. 
```

```
   57  pwd 
```

Run your Java program.
```
   58  java html/MakePage 
```

Refresh your browser. Make sure that you are trying to access **http://<your-address-here>**. It will not work with **https**.

