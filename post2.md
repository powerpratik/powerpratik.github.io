# Ubuntu_Mac_File_Transfer
This repo helps you transfer file between Ubuntu and Mac with the click of a button.

# Mac Ubuntu File Transfer 

 This is the readme for the convinient file transfer for two different OS. In this case, I have Mac and Ubuntu.
This makes it convinient to transfer the files and folders between Ubuntu/Mac in as easy step as putting the required files to the folder To_* and double clicking the copy.sh to send it to the target OS.
 
 
## Structure:
These are the files and directories needed for each OS. This can be found on this repo.

### In Mac:
1) In_Mac directory <br>
2) To_Ubuntu directory <br>
3) copy.sh <br>

### In Ubuntu

1) In_Ubuntu directory <br>
2) To_Mac directory <br>
3) copy.sh <br>

## Step 1:

Copy the files to each of the OS directory. In my case, I have copied to the Downloads directory, but you can do it anywhere. Make sure to update the path in the copy.sh, which will be covered in the coming section.

## Step 2:

Update the copy.sh in each OS by: <br>
a) updating the search_dir variable to the origin system location where the ssh_communication is present. <br>
b) update the user@host_ip with the target system user and ip along with the path to the ssh_communication in the target system.

eg:- For Ubuntu system: <br>
	Part a) would mean updating the search_dir variable to path/to/ssh_communication in ubuntu. <br>
	Part b) would mean updating the user and host_ip with Mac's host_ip and the path tp ssh_communication in Mac.
	
<br>
### Note: This process is to be done in both the OS.

## Step 3:
This method uses ssh to send the files between the OS. 
Make sure you have ssh ready and working in both system. It should be there by default but if not.<br>
(follow https://www.ssh.com/academy/ssh/copy-id)  for step wise guide.
1) use 'ssh-keygen ' to generate private public key pair  <br>
2) Send the key to target os so that you do not need password to access the system. MAKE SURE THIS IS YOUR OWN OS, you do not want to give password less ssh access to system which is not yours. <br>
ssh-copy-id -i ~/.ssh/mykey user@host <br>
3) Test the key using :
	ssh -i ~/.ssh/mykey user@host 
	<br>
### Do this for both the OS	
## Step 4:
You are pretty much good to go.
Make sure to copy the files to the folder that says TO_*  and run the copy.sh using bash.sh

## Step 5 (Optional):

Instead of calling the copy.sh from command line, you can make it executatble such that you can double click copy.sh and send the file to target device.
In the target device the folder In_* contains the sent files and folders
<br>
### use chmod +x copy.sh in mac and ubuntu to make the file executatble.
### In ubuntu make sure to also right-click the copy-sh -> click properties -> Permissions -> Check 'Allow executing file as program' -> Apply and Close.

This is it. follow step 4 to send and receive the files to the target OS but now you can double click the executable file instead of using bash to invoke the command.
