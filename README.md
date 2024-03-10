</h1> Basic Security GPO</h1>

<h2>Description</h2>
In this lab we're going to use Group Policy (GPO). 
<br />
This lab will be split into five parts



- <b>Part 1:​ Creating and assigning a new Group Policy Object</b>
- <b>Part 2:​ Mapping network drives with Group Policy</b>
- <b>Part 3:​ Viewing the setting currently enabled inside a GPO</b>
- <b>Part 4:​ Viewing the GPOs currently assigned to a computer</b> 
- <b>Part 5:​ Backing up and restoring GPOs</b> 

<h2>Environments Used </h2>

- <b>Active Directory</b> 

<h2>Part 1: Creating and assigning a new Group Policy Object​</h2> 
In order to start using Group Policy, we first need to create a Group Policy Object. Most commonly referred to as a GPO, this object contains the settings that we want to deploy. It also contains the information necessary for domain-joined systems to know which machines and users get these settings and which ones do not. It is critical that you plan GPO assignment carefully. It is easy to create a policy that applies to every domain-joined system in your entire network but, depending on what settings you configure in that policy, this can be detrimental to some of your servers. Often, admins who are only somewhat familiar with Group Policy are making use of a built-in GPO called Default Domain Policy. This, by default, applies to everything in your network. Sometimes this is actually what you want to accomplish. Most of the time, it is not! We are going to use this section to detail the process of creating a new GPO, and use some assignment sections called ​Links ​and ​Security Filters​, which will give us complete control over which systems receive these systems, and more importantly, which do not. 
Follow these steps to create and assign a new GPO: 
Open “​Server Manager​”, click on the ​“Tools” ​menu and choose to open the ​“Group Policy Management” ​Console. 
Expand your domain name and click on the folder called ​“Group Policy Objects​”. This shows you a list of your current GPOs. 
Right-click on the “Group Policy Objects” ​​folder and click on ​“New​”. 
Insert a name for your new GPO. Name it “Map Network Drives”. We will end up using this GPO later. 
		 
Click ​“OK”​, and then expand your ​“Group Policy Objects” ​folder if it isn't already. You should see the new GPO in this list. Go ahead and click on the new GPO in order to see its settings.
For this Map Network Drives policy, we want it to apply to the OU called “Users”, under “New York🡪Sales​”.


Right-click on the OU called ​“Users”, under “New York🡪Sales” ​and then click on the option for ​“Link an Existing GPO...​. “
 
Choose the name of our new GPO, “​Map Network Drives”​, and click ​“OK”​. 
 
Our new GPO is now linked to the ​“Users”, OU under “New York🡪Sales” ​OU, so at this level, any system placed inside that OU would get the settings. 
In our example, we created a new Group Policy Object. Each network is different, and you may find yourself relying only on the Links to keep GPOs sorted according to your needs, or you may need to enforce some combination of both Links and Security Filtering. In any case, whichever works best for you, make sure that you are confident in the configuration of these fields so that you can know beyond a shadow of a doubt where your GPO is being applied. You may have noticed that here, we didn't actually configure any settings inside the GPO, so at this point, it still isn't doing anything. Continue this lab to navigate the actual settings portion of Group Policy.	 
<h2>Part 2: Mapping network drives with Group Policy​</h2>	 
Almost everyone uses mapped drives of some flavor in their environments. Creating drive mappings manually as part of a new user start-up process is cumbersome and unnecessary. It is also work that will probably need to be duplicated as users move from one computer to another in the future. If we utilize Group Policy to centralize the creation of these drive mappings, we can ensure that the same users get the same drive mappings wherever they log into the network. Planned correctly, you can enable these mappings to appear on any domain-joined system across the network by the user simply logging in to the computer like they always do. This is a good, simple first task to accomplish within Group Policy to get our feet wet and to learn something that could turn out to be useful in your organization. 
Create a folder called “Sales” on the server’s Drive c: (Note that in a real environment the shared folder will not be located here). 
Right click on the Sales folder, select Properties from the pop-up menu.

On the Sales Properties window, select the “Sharing” tab, and click on the “Advanced Sharing…”, button.

Check the “Share this folder” checkbox, and add a ‘$’ to the end of the share name in order to make this a hidden share. Then click on the “Permissions” button.



On the Permissions for Sales$ window, Remove the Group everyone from the Group or user names: box, and add the group “GRP_Sales_Users”. Make sure GRP_Sales_Users has “Full control” over the share. Click on the “OK” button.

Back on the Advanced Sharing window, click on the OK button. 

Back on the Sales Properties window, click on the Close button.



To create a drive mapping in Group Policy: 
Open the ​“Group Policy Management” ​Console from the “​Tools” ​menu of Server Manager. 
Expand the name of your domain and then expand the ​“Group Policy Objects” ​folder. 
	There we see our new GPO called “Map Network Drives”​	​. 
Right-click on the “Map Network Drives” ​GPO and click on “​Edit...​. “
 
Navigate to ​“User Configuration ​| ​Preferences ​| ​Windows Settings ​| Drive Maps​”	​. 
Right-click on ​“Drive Maps” ​and choose “​New ​| ​Mapped Drive​”. 
 
Set ​“Location” ​as the destination URL (\\Server1\Sales$) of the drive mapping, and use the ​“Label as” ​field if you want a more descriptive name to be visible to users. 
Choose a “​Drive Letter” ​to be used for this new mapping from the drop-down menu listed on this screen. 

Click ​“OK”​. 
i.	We are assuming you have already created the Links appropriate to where you want this GPO to apply. If so, you may now login using the Win 10 Lab VM client computer with a user that is part of the sales team. Once logged into the computer, open up “File Explorer” and you should see the new network drive mapped automatically during the login process. 
			 
There are a few different ways that drive mappings can be automated within a Windows environment, and our lab today outlines one of the quickest ways to accomplish this task. By using Group Policy to automate the creation of our network drive mappings, we can centralize the administration of this task and remove the drive mapping creation load from our helpdesk processes






Submission instructions:
Please describe your work and take screenshots of every step you do. Create a document with all the screenshots and explanations and upload the file. 


Part 3 and on is not mandatory, we strongly recommend you explore this, but no need to submit anything on the following sections.
  
<h2>Part 3: Viewing the setting currently enabled inside a GPO​<h2>	 
So far, we have been creating GPOs and putting settings into them, so we are well aware of what is happening with each of our policies. Many times, though, you enter a new environment that contains a lot of existing policies, and you may need to figure out what is happening in those policies. We have seen many cases where you install a new server, join it to the domain, and it breaks. It doesn't necessarily nose dive, but some component won't work properly or you can't flow network traffic to it for some reason. Something like that can be hard to track down. Since the issue seemed to happen during the domain join process, most would suspect that some kind of policy from an existing GPO has been applied to the new server and is having a negative effect on it. Let's take a look inside Group Policy at the easiest way to display the settings that are contained within each GPO. 
For this lab, we only need access to the Group Policy Management Console, which we are going to run from our Win Server 2016 Lab VM domain controller server. 
To quickly view the settings contained within a GPO, follow these steps: 
In the Domain Controller, open up Server Manager and launch the Group Policy​	 
	Management Console from inside the ​	Tools ​	menu.​	 
Expand the name of your domain, then expand the ​Group Policy Objects ​folder. This displays all of the GPOs currently configured in your domain. 
Click on one of the GPOs so that you see the ​Links ​and ​Security Filtering ​sections in the right window pane. 
Now click on the ​Settings ​tab near the top. 
Once you have ​Settings ​tab open, click on the ​show all ​link near the top right. This will display all of the settings that are currently configured inside that GPO. 
			 
 	 	 
In this very simple lab, we use the Group Policy Management Console in order to view the currently configured settings inside our GPOs. This can be very useful for checking over existing settings and for comparing them against what is actually being configured on the client computers. Taking a look through this information can also help you to spot potential problems, such as duplicate settings spread across multiple GPOs. 
Viewing the settings included in a GPO can be helpful during troubleshooting, but there are many other tools that can be additionally used in order to troubleshoot Group Policy. Here are a couple of links to help you understand the recommended procedures for troubleshooting Group Policy: 
​http://technet.microsoft.com/en-us/library/jj134223.aspx 
http://technet.microsoft.com/en-us/library/cc749336%28v=ws.10%29.aspx 
<h2>Part 4: Viewing the GPOs currently assigned to a computer<h2>
Once you start using Group Policy to distribute settings around to many client computers, it will quickly become important to be able to view the settings and policies that have or have not been applied to specific computers. Thankfully, there is a command built right into the Windows operating system to display this information. There are a number of different switches that can be used with this command, so let's explore some of the most common ones seen and used by server administrators. 
We have a number of GPOs in our domain now; some are applied at the top level of the domain and some are only applied to specific OUs. We are going to run some commands on our Server 2016 server in order to find out which GPOs have been applied to it and which have not. 
Let's use the ​gpresult​ command to gather some information on policies applied to our server: 
Log in to the web server, or whatever client computer (You can use the Win 10 Lab VM)  you want to see these results on, and open up an administrative Command Prompt. 
Type ​gpresult /r​ and press Enter​. This displays all of the resultant data on which policies are applied, and are not applied, to our system. You can scroll through this information to get the data that you need. 
Now let's clean that data up a little bit. For instance, the general output we just received had information about both computer policies and user policies. Now we want to display only policies that have applied at the User level. Go ahead and use this command: 
gpresult /r /scope:user​. 
		 
You can use either the ​/SCOPE:USER switch or the ​​/SCOPE:COMPUTER ​switch in order to view specifically the user or computer policies applied to the system. 
And if you aren't a huge fan of looking at this data via a command prompt, never fear! There is another switch that can be used to export this data to HTML format. Try the following command:​ gpresult /h c:\gpresult.html
After running that command, browse to your​ C:​ drive and you should have a file sitting there called ​gpresult.html​. Go ahead and open that file to see your gpresult data in a web browser with a nicer look and feel. 
		 
The gpresult command can be used in a variety of ways to display information about which Group Policy Objects and settings have been applied to your client computer or server. This can be especially useful when trying to determine what policies are being applied, and maybe even more helpful when trying to figure out why a particular policy hasn't been applied. If a policy is denied because of rights or permissions, you will see it in this output. This likely indicates that you have something to adjust in your Links or Security Filtering in order to get the policy applied successfully to your machine. However you decide to make use of the data for yourself, make sure to play around with the gpresult command and get familiar with its results if you intend to administer your environment using Group Policy. 
One additional note about another command that is very commonly used in the field. Windows domain joined machines only process Group Policy settings every once in a while; by default they will refresh their settings and look for new policy changes every 90 minutes. If you are creating or changing policies and notice that they have not yet been applied to your endpoint computers, you could hang out for a couple of hours and wait for those changes to be applied. If you want to speed up that process a little, you can log in to the endpoint client computer, server, or whatever it is that should receive the settings, and use the gpupdate /force command. This will force that computer to revisit Group Policy and apply any settings that have been configured for it. When we make changes in the field and don't want to spend a lot of time waiting around for replication to happen naturally, we often use gpupdate /force numerous times as we make changes and progress through testing.  
Some prefer gpresult to view the policies that are currently applied to a computer that they are working on, but it's not the only way. You may also want to check out RSOP.MSC​. This is a tool that can be launched in order to see a more visually stimulating version of the policies and settings that are currently applied to your computer. Check out the details here: 
	a.	http://technet.microsoft.com/en-us/library/cc772175.aspx 
<h2>Part 5: Backing up and restoring GPOs​</h2>
As with any piece of data in your organization, it is a good idea to keep backups of your GPOs. Keeping these backups separately from a full Domain Controller or full Active Directory backup can be advantageous, as it enables a quicker restore of individual GPOs in the event of an accidental deletion. Or perhaps you updated a GPO, but the change you made is now causing problems and you want to roll that policy back to make sure it is configured the way that it was yesterday. Whatever your reason for backing up and restoring GPOs, let's take a look at a couple of ways to accomplish each task. We will use the Group Policy Management Console to perform these functions. 
We are going to perform these tasks from a Windows Server 2016 domain controller in our environment. We will utilize the Group Policy Management Console. 
There is a GPO in our domain called ​Map Network Drives​. Let’s use Group Policy Management Console to backup and restore this GPO: 
From the ​Tools ​menu of Server Manager, open up the ​Group Policy Management Console. 
Navigate to ​Forest ​| ​Domains ​| Your Domain Name ​	| ​ ​Group Policy Objects​. 
If you want to backup a single GPO, you simply right-click on the specific GPO and choose ​Back Up...​. Otherwise, it is probably more useful for us to back up the whole set of GPOs. To accomplish that, right-click on the ​Group Policy Objects ​folder and then choose Back Up All...​	​. 
	i	 
d.	Specify a location where you want the backups to be saved and a description for the backup set. Then click ​Back Up​. 
		 
Once the backup process is complete, you should see the status of how many GPOs were successfully backed up. 
		 
Now that we have a backup of the GPOs, let's try to restore the GPO called ​Map Network Drives​. 
Navigate back inside the ​Group Policy Management ​Console and find the ​Group Policy Objects ​folder. The same location that we used to backup a minute ago. 
Right-click on the ​Map Network Drives ​GPO and choose ​Restore from Backup...​. 
 
Click ​Next ​and specify the folder where your backup files are stored. Then click ​Next again. 
As long as a backup copy of the ​Map Network Drives GPO exists in that folder, you will​	 see it in the wizard. Select that GPO and click ​Next​. 
		 
Click ​Finish ​and the GPO will be restored to its previous state. 
	4.	Backing up and restoring GPOs is going to be a regular task for anybody administering Active 
Directory and Group Policy. In this lab, we walked through the process. Group Policy 
Management Console is nice because it is graphically interfaced, and it is easy to look at the options available to you. 
