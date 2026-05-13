Tags: [[__Data_Engineering]], [[__Machine_Learning_Engineering]], [[__Programming_languages]]

# Introduction
This repository contains simple, universal and useful Python scripts.
# Code repository
Repository with the code - [github.com](https://github.com/bulka4/useful_python_scripts).
## recursive_function.py
That script helps to understand how the recursive function works. We have here a recursive function that returns a full path to the folder 
with specified folder ID.

That function is looking for a specified folder in a nested JSON which represents a folder structure. It looks like that:
```
{
    'id': folder_id
    ,'name': root_folder # folder_name
    ,'folders': [folder_object_1, folder_object_2, ....]
}
```
where folder_object_1, folder_object_2 etc represents other folders contained in that folder and has the same format as the JSON above.

That JSON is provided to the function as the folders_object argument.

As a level we define how 'deep' in folders we are, how many layers below the root folder. It looks like that:

```
root_folder       <- level 1
|-- folder_1      <- level 2
|-- |-- folder_2  <- level 3
|-- folder_3      <- level 2
```

Each recursive call of this function happens on a specific level, in a specific folder. First it checks if the current folder is the one
we are looking for, then it starts looking in all the subfolders (it goes to a lower level). For each subfolder we make another
recursive call of this function.

In our example folder structure this function might perform the following recursive calls:
- The first recursive function call: 
    - Check if the current folder, on level 1, is the one we are looking for -> folder not found
    - Make the second recursive function call: 
        - Check if the current folder, folder_1 on level 2, is the one we are looking for -> folder not found
        - Make the third recursive function call:
            - Check if the current folder, folder_2 on level 3, is the one we are looking for -> folder not found
        - We go back to the second recursive function call. Now we check the folder_3, on level 2 -> folder found.
    - We go back to the second recursive function call. We get information from the third recursive call that the folder has been found and the path to folder.
- We go back to the first recursive function call. We get information from the second recursive call that the folder has been found and we are returning the path to that folder.

In that script there is written an example JSON representing a folder structure and we are calling there this function to print a path
to a folder with specified ID.