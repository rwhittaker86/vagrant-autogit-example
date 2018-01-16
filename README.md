# vagrant-autogit-example
and example of how to use Vagrant &amp; vagrant-trigger to automate git commit &amp; push on Vagrant destroy/halt/suspend

<h1>Vagrant git automation</h1>
<p>This repo contains a simple example of how to implement git workflow integration using Vagrant and the vagrant-triggers plugin</p>
<h2>How To Use This Example as a Template</h2>
<p>In this example I am using the ubuntu/trusty64 <a href="https://app.vagrantup.com/ubuntu/boxes/trusty64">found here</a> to setup a simpe ubuntu server dev environment</p>
<p>to use a different Vagrant box just change the second line of the Vagrantfile to relfect the box that you woould like to use</p>
<p>For this template to work you will need to have the vagrant-triggers plugin installed on your host machine which can be found <a href="https://github.com/emyl/vagrant-triggers">here</a> along with documentation ond other some basic examples</p>
<h3>Make It Your Own</h3>
<p>For this template to work properly you will need to change the following:
<ul>
<li>Use your own information for user.email and user.name in bootstrap.sh on lines 10 and 11</li>
<li>Use your github info in the cleanup.sh on line 10</li>
</ul>
Note that on lines 7 and 8 the bootstrap.sh and cleanup.sh are set to untracked by git, this is to protect your personal information in the event that you might use this template for a project stored in a public repository</p>
<h2>How it works</h2>
<p>The bootstrap.sh script runs on provisioning the Vagrant box which is standard Vagrant funcitonality (Documentation can be found <a href="https://www.vagrantup.com/intro/getting-started/provisioning.html">here</a>).
bootstrap.sh in the example installs apache, sets the web root to the synced folder, installs git, then sets required git config. This way your environment is ready to go for a 'blank slate' ubuntu server</p>
<h3>Now for The Fun Part</h3>
<p>Now if you look in the Vagrantfile you will see the triggers bound to the suspend, halt, and destroy Vagrant events. Here vagrant-triggers is used to run the cleanup.sh script when any of these events are fired.</p>
<p>In cleanup.sh the conditional on git status --porclain is used as a placeholder in the event that there are certain git status output that you would like to fire the add, commit, push sequence upon.
In this example as-is the sequence will fire everytime</p>
<p>The sequence that follows simply adds all changes made within the synced folder, then removes the .vagrant/ folder and scripts that may contain personal info, and finally commits and pushes the update with a placeholder commit message</p>
<p>Ideally by using this example you should always have the work you have completed in your Vagrant box backedup in git which makes the portable nature of Vagrant even simpler.</p>
<p>I hope that you find this simple example to be useful!</p>
<p>Please feel free to fork and possibly contribute if you feel you can augment this example, and kindly forgive my inexperience as I am fairly new to using Vagrant</p> 
