Tags: [[_Python]] [[__Programming_languages]]
#Python #ProgrammingLanguages 

# Isolation from system packages
When we install a package using `pip`, the same package in a different version might already be installed in the system, installed with different tool than `pip`, for example `apt-get`. 

In that case, `pip` will try to uninstall it and install another version and it will fail, because `pip` didn't install it so it can't uninstall it (it doesn't know where are files of that package).

But if we install that package using `pip` in a virtual environment, then it will not be trying to uninstall the same, existing package, because that existing package is outside of the virtual environment, so we will avoid that error.