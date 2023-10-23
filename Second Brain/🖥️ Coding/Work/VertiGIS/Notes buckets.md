```toc
```

# Search Designer

## Schema - Schema validator 

Some of the components in the search Designer are *Built* using the Schema. For example we have the `app-config.schema.ts` and tha schema defines how the UI will look like. 
For example the types of Schema we have is: 
- `select`
- `group`
- `checkbox`
- `label`
- `number`
- `text
- `toggle`

as we can see those are mostly inputs which we can define in the schema and have them show up on the UI. 

Studio Web uses the same approach, however, our version is a bit simpler and has some features the web version does not have. For example, the validation is not that sophisticated as the one in the Studio Web Designer. However We have a specific attribute on the `group` type which helps us to "split" the views. So we can have 2 settings side by side. Also the `split` attribute can be added to other types to we can split it even further. 

Example of split in Search Designer: 
![image info](./Pasted image 20220908130532.png)
![[Pasted image 20220908130532.png]]

and in the code it looks like this: 

![image](./Pasted image 20220908130610.png)

So to split the inputs on a specific input we can use the `split: true` attribute. 


## ControlContainer component

To render the schema we defined above we need to "Feed" into the `ControlContainer` component: 

![Image](./Pasted image 20220908131729.png)


What `ControlContainer` will do is take the schema and see what kind of attributes are in the schema and depending on that if its a `group` or just a setting example `label` it will either render the `<GroupControl>` component or the `SettingControl`.

`ControLContainer` can be called / used anywhere so we can set it up wherever we want. 


## Extending

If we want to extend the inputs defined we have to extend the `SettingsControl` and add additional `control` components for the extended setting. 

Also we need to extend the interfaces for the new control: 
![[Pasted image 20220908142315.png]] 
ex. `interface datePicker` if we want to add a new datepicker control. 


