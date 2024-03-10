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
- <b>Command Prompt</b>
- <b>File Explorer</b>

<h2>Part 1: Creating and assigning a new Group Policy Object​</h2> 
In order to start using Group Policy, we first need to create a Group Policy Object. Most commonly referred to as a GPO, this object contains the settings that we want to deploy. It also contains the information necessary for domain-joined systems to know which machines and users get these settings and which ones do not. It is critical that you plan GPO assignment carefully. It is easy to create a policy that applies to every domain-joined system in your entire network but, depending on what settings you configure in that policy, this can be detrimental to some of your servers. Often, admins who are only somewhat familiar with Group Policy are making use of a built-in GPO called Default Domain Policy. This, by default, applies to everything in your network. Sometimes this is actually what you want to accomplish. Most of the time, it is not! We are going to use this section to detail the process of creating a new GPO, and use some assignment sections called ​Links ​and ​Security Filters​, which will give us complete control over which systems receive these systems, and more importantly, which do not. 
<br />	

Follow these steps to create and assign a new GPO: 
<br />	

Open “​Server Manager​”, click on the ​“Tools” ​menu and choose to open the ​“Group Policy Management” ​Console. 
<br />	

Expand your domain name and click on the folder called ​“Group Policy Objects​”. This shows you a list of your current GPOs. 
<br />	

Right-click on the “Group Policy Objects” ​​folder and click on ​“New​”. 
<br />	

Insert a name for your new GPO. Name it “Map Network Drives”. We will end up using this GPO later. 

<img src="https://i.imgur.com/spWPj7b.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	

Click ​“OK”​, and then expand your ​“Group Policy Objects” ​folder if it isn't already. You should see the new GPO in this list. Go ahead and click on the new GPO in order to see its settings.
<br />	

For this Map Network Drives policy, we want it to apply to the OU called “Users”, under “New York🡪Sales​”.
<br />	

Right-click on the OU called ​“Users”, under “New York🡪Sales” ​and then click on the option for ​“Link an Existing GPO...​. “

<img src="https://i.imgur.com/oSKhs30.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Choose the name of our new GPO, “​Map Network Drives”​, and click ​“OK”​. 

<img src="https://i.imgur.com/oOCGZjb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Our new GPO is now linked to the ​“Users”, OU under “New York🡪Sales” ​OU, so at this level, any system placed inside that OU would get the settings. 
<br />

In our example, we created a new Group Policy Object. Each network is different, and you may find yourself relying only on the Links to keep GPOs sorted according to your needs, or you may need to enforce some combination of both Links and Security Filtering. In any case, whichever works best for you, make sure that you are confident in the configuration of these fields so that you can know beyond a shadow of a doubt where your GPO is being applied. You may have noticed that here, we didn't actually configure any settings inside the GPO, so at this point, it still isn't doing anything. Continue this lab to navigate the actual settings portion of Group Policy.
<br />


<h2>Part 2: Mapping network drives with Group Policy​</h2>	 
Almost everyone uses mapped drives of some flavor in their environments. Creating drive mappings manually as part of a new user start-up process is cumbersome and unnecessary. It is also work that will probably need to be duplicated as users move from one computer to another in the future. If we utilize Group Policy to centralize the creation of these drive mappings, we can ensure that the same users get the same drive mappings wherever they log into the network. Planned correctly, you can enable these mappings to appear on any domain-joined system across the network by the user simply logging in to the computer like they always do. This is a good, simple first task to accomplish within Group Policy to get our feet wet and to learn something that could turn out to be useful in your organization. 
<br />

Create a folder called “Sales” on the server’s Drive c: (Note that in a real environment the shared folder will not be located here). 
<br />

Right click on the Sales folder, select Properties from the pop-up menu.

<img src="https://i.imgur.com/4i47bHQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

On the Sales Properties window, select the “Sharing” tab, and click on the “Advanced Sharing…”, button.

<img src="https://i.imgur.com/9ZgM7KV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Check the “Share this folder” checkbox, and add a ‘$’ to the end of the share name in order to make this a hidden share. Then click on the “Permissions” button.
<br />
<img src="https://i.imgur.com/AAlq0EG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />


On the Permissions for Sales$ window, Remove the Group everyone from the Group or user names: box, and add the group “GRP_Sales_Users”. Make sure GRP_Sales_Users has “Full control” over the share. Click on the “OK” button.
<br />
<img src="https://i.imgur.com/OYqGXqr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Back on the Advanced Sharing window, click on the OK button.
<br />
<img src="https://i.imgur.com/SwHXcWo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />


Back on the Sales Properties window, click on the Close button.
<br />
<img src="https://i.imgur.com/yyfuklG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

To create a drive mapping in Group Policy: 
Open the ​“Group Policy Management” ​Console from the “​Tools” ​menu of Server Manager. 
<br />

Expand the name of your domain and then expand the ​“Group Policy Objects” ​folder. 
	There we see our new GPO called “Map Network Drives”​	​
<br />

Right-click on the “Map Network Drives” ​GPO and click on “​Edit...​. “
<br />
<img src="https://i.imgur.com/VQYesoH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Navigate to ​“User Configuration ​| ​Preferences ​| ​Windows Settings ​| Drive Maps​”	​.
<br />

Right-click on ​“Drive Maps” ​and choose “​New ​| ​Mapped Drive​”. 
<br />
<img src="https://i.imgur.com/ptWh0bX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Set ​“Location” ​as the destination URL (\\Server1\Sales$) of the drive mapping, and use the ​“Label as” ​field if you want a more descriptive name to be visible to users. 
<br />

Choose a “​Drive Letter” ​to be used for this new mapping from the drop-down menu listed on this screen. 
<br />

Click ​“OK”​. 
<br />
<img src="https://i.imgur.com/KGpuh4y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

We are assuming you have already created the Links appropriate to where you want this GPO to apply. If so, you may now login using the Win 10 Lab VM client computer with a user that is part of the sales team. Once logged into the computer, open up “File Explorer” and you should see the new network drive mapped automatically during the login process. 
<br />
<img src="https://i.imgur.com/7x0N4Nn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

There are a few different ways that drive mappings can be automated within a Windows environment, and our lab today outlines one of the quickest ways to accomplish this task. By using Group Policy to automate the creation of our network drive mappings, we can centralize the administration of this task and remove the drive mapping creation load from our helpdesk processes
<br />


  
<h2>Part 3: Viewing the setting currently enabled inside a GPO​<h2>	

 
So far, we have been creating GPOs and putting settings into them, so we are well aware of what is happening with each of our policies. Many times, though, you enter a new environment that contains a lot of existing policies, and you may need to figure out what is happening in those policies. We have seen many cases where you install a new server, join it to the domain, and it breaks. It doesn't necessarily nose dive, but some component won't work properly or you can't flow network traffic to it for some reason. Something like that can be hard to track down. Since the issue seemed to happen during the domain join process, most would suspect that some kind of policy from an existing GPO has been applied to the new server and is having a negative effect on it. Let's take a look inside Group Policy at the easiest way to display the settings that are contained within each GPO. 
<br />

For this lab, we only need access to the Group Policy Management Console, which we are going to run from our Win Server 2016 Lab VM domain controller server. 
<br />

To quickly view the settings contained within a GPO, follow these steps: 
<br />

In the Domain Controller, open up Server Manager and launch the Group Policy​	 
Management Console from inside the ​Tools ​menu.​	 
<br />

Expand the name of your domain, then expand the ​Group Policy Objects ​folder. This displays all of the GPOs currently configured in your domain. 
<br />

Click on one of the GPOs so that you see the ​Links ​and ​Security Filtering ​sections in the right window pane. 
<br />

Now click on the ​Settings ​tab near the top. 
<br />

Once you have ​Settings ​tab open, click on the ​show all ​link near the top right. This will display all of the settings that are currently configured inside that GPO. 
<br />
<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />			 
 	 	 
In this very simple lab, we use the Group Policy Management Console in order to view the currently configured settings inside our GPOs. This can be very useful for checking over existing settings and for comparing them against what is actually being configured on the client computers. Taking a look through this information can also help you to spot potential problems, such as duplicate settings spread across multiple GPOs. 
<br />	

<h2>Part 4: Viewing the GPOs currently assigned to a computer<h2>
<br />	
	
Once you start using Group Policy to distribute settings around to many client computers, it will quickly become important to be able to view the settings and policies that have or have not been applied to specific computers. Thankfully, there is a command built right into the Windows operating system to display this information. There are a number of different switches that can be used with this command, so let's explore some of the most common ones seen and used by server administrators. 
<br />	

We have a number of GPOs in our domain now; some are applied at the top level of the domain and some are only applied to specific OUs. We are going to run some commands on our Server 2016 server in order to find out which GPOs have been applied to it and which have not. 
Let's use the ​gpresult​ command to gather some information on policies applied to our server: 
<br />	

Log in to the web server, or whatever client computer (You can use the Win 10 Lab VM)  you want to see these results on, and open up an administrative Command Prompt. 
<br />	

Type ​gpresult /r​ and press Enter​. This displays all of the resultant data on which policies are applied, and are not applied, to our system. You can scroll through this information to get the data that you need. 
<br />	

Now let's clean that data up a little bit. For instance, the general output we just received had information about both computer policies and user policies. Now we want to display only policies that have applied at the User level. Go ahead and use this command: 
gpresult /r /scope:user​. 
<br />
<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
		 
You can use either the ​/SCOPE:USER switch or the ​​/SCOPE:COMPUTER ​switch in order to view specifically the user or computer policies applied to the system. 
<br />

And if you aren't a huge fan of looking at this data via a command prompt, never fear! There is another switch that can be used to export this data to HTML format. Try the following command:​ gpresult /h c:\gpresult.html
<br />

After running that command, browse to your​ C:​ drive and you should have a file sitting there called ​gpresult.html​. Go ahead and open that file to see your gpresult data in a web browser with a nicer look and feel.
<br />
<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
		 
The gpresult command can be used in a variety of ways to display information about which Group Policy Objects and settings have been applied to your client computer or server. This can be especially useful when trying to determine what policies are being applied, and maybe even more helpful when trying to figure out why a particular policy hasn't been applied. If a policy is denied because of rights or permissions, you will see it in this output. This likely indicates that you have something to adjust in your Links or Security Filtering in order to get the policy applied successfully to your machine. However you decide to make use of the data for yourself, make sure to play around with the gpresult command and get familiar with its results if you intend to administer your environment using Group Policy. 
<br />

One additional note about another command that is very commonly used in the field. Windows domain joined machines only process Group Policy settings every once in a while; by default they will refresh their settings and look for new policy changes every 90 minutes. If you are creating or changing policies and notice that they have not yet been applied to your endpoint computers, you could hang out for a couple of hours and wait for those changes to be applied. If you want to speed up that process a little, you can log in to the endpoint client computer, server, or whatever it is that should receive the settings, and use the gpupdate /force command. This will force that computer to revisit Group Policy and apply any settings that have been configured for it. When we make changes in the field and don't want to spend a lot of time waiting around for replication to happen naturally, we often use gpupdate /force numerous times as we make changes and progress through testing.  
<br />

Some prefer gpresult to view the policies that are currently applied to a computer that they are working on, but it's not the only way. You may also want to check out RSOP.MSC​. This is a tool that can be launched in order to see a more visually stimulating version of the policies and settings that are currently applied to your computer. Check out the details here: 
	a.	http://technet.microsoft.com/en-us/library/cc772175.aspx 
 <br />
 
<h2>Part 5: Backing up and restoring GPOs​</h2>
<br />

As with any piece of data in your organization, it is a good idea to keep backups of your GPOs. Keeping these backups separately from a full Domain Controller or full Active Directory backup can be advantageous, as it enables a quicker restore of individual GPOs in the event of an accidental deletion. Or perhaps you updated a GPO, but the change you made is now causing problems and you want to roll that policy back to make sure it is configured the way that it was yesterday. Whatever your reason for backing up and restoring GPOs, let's take a look at a couple of ways to accomplish each task. We will use the Group Policy Management Console to perform these functions. 
<br />

We are going to perform these tasks from a Windows Server 2016 domain controller in our environment. We will utilize the Group Policy Management Console. 
<br />

There is a GPO in our domain called ​Map Network Drives​. Let’s use Group Policy Management Console to backup and restore this GPO: 
<br />

From the ​Tools ​menu of Server Manager, open up the ​Group Policy Management Console. 
Navigate to ​Forest ​| ​Domains ​| Your Domain Name ​| ​​Group Policy Objects​. 


If you want to backup a single GPO, you simply right-click on the specific GPO and choose ​Back Up...​. Otherwise, it is probably more useful for us to back up the whole set of GPOs. To accomplish that, right-click on the ​Group Policy Objects ​folder and then choose Back Up All...​	
​<br />
<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	 
	 
Specify a location where you want the backups to be saved and a description for the backup set. Then click ​Back Up​. 

<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	

Once the backup process is complete, you should see the status of how many GPOs were successfully backed up. 

<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	

Now that we have a backup of the GPOs, let's try to restore the GPO called ​Map Network Drives​. 
<br />

Navigate back inside the ​Group Policy Management ​Console and find the ​Group Policy Objects ​folder. The same location that we used to backup a minute ago. 
<br />

Right-click on the ​Map Network Drives ​GPO and choose ​Restore from Backup...​. 

<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	

Click ​Next ​and specify the folder where your backup files are stored. Then click ​Next again. 
<br />

As long as a backup copy of the ​Map Network Drives GPO exists in that folder, you will​	 see it in the wizard. Select that GPO and click ​Next​. 

<img src="https://i.imgur.com/YcQQTAe.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />	

Click ​Finish ​and the GPO will be restored to its previous state. 
<br />

Backing up and restoring GPOs is going to be a regular task for anybody administering Active 
<br />

Directory and Group Policy. In this lab, we walked through the process. Group Policy 
Management Console is nice because it is graphically interfaced, and it is easy to look at the options available to you. 
<br />
