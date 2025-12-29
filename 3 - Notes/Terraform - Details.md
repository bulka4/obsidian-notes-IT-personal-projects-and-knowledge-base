Tags: [[__Cloud]], [[__DevOps]], [[__Infrastructure_Engineering]]

# Useful resources

## Azurerm_virtual_machine_extension

Execute a bash script on a VM using Azure VM extension.

When we are creating a VM using Terraform we can also execute a bash script on that VM right after creating it also using this Terraform resource.

More info about how to run a bash script using the virtual machine extension here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/custom-script-linux).

We can use the templatefile function in order to insert variables into a bash script and then run that script on a VM using the azurerm_virtual_machine_extension resource:
![[2 - Images/Terraform - Details/Screenshot 1.png]]

### Debugging

Logs from executing a bash script on VM can be found on that VM in the /var/lib/waagent/custom-script/download/0 folder. There are the 'stdout' and 'stderr' files with logs. More info about that here: [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/troubleshoot).

# Useful functions

## Templatefile

Insert variables into a file (interpolation, rendering).

# Working with strings (heredoc, escape sequences etc)

When working with strings, for example in comments, files passed to the templatefile function, there are usefull functions for that decribed here: [link](#strings-and-templates). There are described for example escape sequences, heredoc strings.