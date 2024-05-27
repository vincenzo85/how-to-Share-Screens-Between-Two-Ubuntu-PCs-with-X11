# how-to-Share-Screens-Between-Two-Ubuntu-PCs-with-X11
Share Screens Between Two Ubuntu PCs with X11
### Title
How to Share Screens Between Two Ubuntu PCs with X11: A Step-by-Step Guide

### SEO Description
Discover how to configure screen sharing between two Ubuntu PCs using X11. Our detailed guide covers installation, X11 forwarding, authentication, and troubleshooting with a user-friendly approach.

### LinkedIn Post
🔧 Looking to level up your tech skills? 🔧

Ever wished you could seamlessly share your screen between two Ubuntu PCs? 🖥️➡️🖥️

Say goodbye to complicated setups and hello to X11 magic! In our latest guide, we break down the process step-by-step, ensuring even the most non-techie among us can follow along. Whether you're working on a project, delivering a presentation, or just want to streamline your workflow, this guide has got you covered.

Get ready to:
1️⃣ Install and set up X2X and X11.
2️⃣ Configure SSH for X11 forwarding.
3️⃣ Troubleshoot common issues with ease.

Ready to dive in? Check out the full article and become the screen-sharing wizard you were always meant to be! 🌟

#Ubuntu #ScreenSharing #TechTips #X11 #Linux #Productivity

---

### Article: How to Share Screens Between Two Ubuntu PCs with X11

Hey there, tech enthusiasts! 🎉 Looking to level up your Ubuntu game? We've got a fun and super useful guide for you today: sharing screens between two Ubuntu PCs using X11. Forget about boring, clunky setups—this one's smooth and sleek. Ready? Let’s dive in!

#### Why X11?
Before we jump into the nitty-gritty, why bother with X11? Well, if you're looking to control one PC from another, whether it’s for development, presentations, or just plain fun, X11 has got your back. Plus, it's open-source and packed with powerful features. Who doesn’t love a good open-source tool?

### Step 1: Install X2X and X11

First things first, let’s get the essentials installed on both your primary and secondary computers.

On **both** computers:
```bash
sudo apt update
sudo apt install x2x xorg
```
Easy, right? Now we’re all set to start configuring.

### Step 2: Configure X11 Forwarding

Alright, let’s move on to enabling X11 forwarding. This step is crucial for making sure X2X works its magic.

On the **secondary** computer:
1. Open the SSH configuration file:
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
2. Ensure the following lines are present and uncommented:
    ```plaintext
    X11Forwarding yes
    X11DisplayOffset 10
    X11UseLocalhost yes
    ```
3. Save and exit the editor (Ctrl + X, then Y, then Enter).
4. Restart the SSH service:
    ```bash
    sudo systemctl restart ssh
    ```

### Step 3: Set Up X Authentication

Next up, we need to make sure the primary computer can access the display of the secondary computer.

On the **secondary** computer:
```bash
xhost +<IP_of_primary_computer>
```
Replace `<IP_of_primary_computer>` with the actual IP address of your primary computer.

### Step 4: Connect via SSH with X11 Forwarding

Now, let’s connect the primary computer to the secondary one using SSH.

On the **primary** computer:
```bash
ssh -X username@<IP_of_secondary_computer>
```
Replace `username` and `<IP_of_secondary_computer>` with your actual username and the IP address of the secondary computer.

To check if everything is set up correctly, verify the DISPLAY environment variable:
```bash
echo $DISPLAY
```
You should see something like `localhost:10.0`.

## What does -X mean in ssh -X?
The -X option in the ssh command enables X11 forwarding. X11 forwarding allows you to run graphical applications on a remote machine and display them on your local machine. Here's a detailed explanation:
X11 Forwarding: X11 is a windowing system for bitmap displays, common on UNIX-like operating systems. Forwarding X11 over SSH allows you to securely run graphical applications installed on a remote machine and view them on your local machine as if they were running locally.
Secure Communication: By using X11 forwarding, the communication between the local and remote machines is encrypted, which is more secure than using X11 without SSH.
## Why use -X?
Running Remote Graphical Applications: You might have software installed on a remote server that you need to use, but it has a graphical user interface (GUI). With X11 forwarding, you can run the application on the remote server and have the GUI displayed on your local machine.
Security: X11 forwarding over SSH provides a secure channel for transmitting graphical data, protecting it from being intercepted or tampered with during transmission.
Convenience: It allows you to use the computational resources of the remote machine while still interacting with the application on your local machine. This can be especially useful for resource-intensive applications.

### Step 5: Test the Setup

Time for the moment of truth! Let’s see if the X11 forwarding is working.

On the **primary** computer:
```bash
xclock
```
If an X11 clock pops up, you’re golden! 🎉

### Step 6: Launch X2X

Finally, let’s launch X2X to control the secondary computer from the primary one.

On the **primary** computer:
```bash
x2x -east -to :0
```
This command assumes the secondary computer’s display is `:0`. Adjust as needed if you’ve got different settings.

### Troubleshooting Tips

If you hit any snags along the way, here are a few things to check:
- Ensure the `.Xauthority` file on the secondary computer is accessible:
    ```bash
    ls -la ~/.Xauthority
    ```
- Manually set the DISPLAY variable on the primary computer:
    ```bash
    export DISPLAY=:0
    ```
- Check SSH logs for X11 forwarding issues:
    ```bash
    sudo tail -f /var/log/auth.log
    ```
- Make sure your firewall isn’t blocking X11 connections (port 6000).

And that’s it! You’re now ready to share screens between two Ubuntu PCs using X11 like a pro. 🖥️💻 If you found this guide helpful, be sure to share it with your fellow Linux enthusiasts. Happy screen sharing!
