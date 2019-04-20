# Aura-Method-in-Lightning-Component
Call Child Component Controller From Parent Component - Aura Method

aura:method: - Use <aura:method> to define a method as part of a component's API. This enables you to directly call a method in a component’s client-side controller instead of firing and handling a component event.

The <aura:method> tag has these system pre defined attributes that we can use

Name: - The method name. Use the method name to call the method in JavaScript code.

Action: - The client-side controller action to execute

Access: - he access control for the method. Valid values are: public and global

Description: - The description of method.

Declaring Parameters: - We can also use parameters to send the values from parent to child using the attributes.

Below is sample of child Component

````

<aura:method name="sampleMethod" action="{!c.doAction}"
                        description="Sample method with parameters">
       <aura:attribute name="param1" type="String" default="parameter 1"/>
       <aura:attribute name="param2" type="String" />
</aura:method>

````

Define the action that needs to be executed when "sampleMethod" gets called from the parent component. Create a method into Controller of Child Component. Child Component Controller sample code.

````

({
doAction : function(cmp, event) {
var params = event.getParam('arguments');
if (params) {
var param1 = params.param1;
// add your code here
}
}
})

````

Get the value into the child controller: - Retrieve the arguments using event.getParam('arguments'). It returns an object if there are arguments or an empty array if there are no arguments. For example if you are passing 2 parameters then you can get like below

Step1: - Get the array of all the arguments

var params = event.getParam('arguments');

Step2: - Now, get the value of the attribute using the name of the attribute.

var param1 = params.param1;

var param2 = params.param2;
In Final Step Call the method from the Parent Code: -

Step1: - Call the child component inside the parent component using the syntax like below and use aura:id for the child component which will let you find the child component and then you can call the controller method.

<c:childComponent aura:id='childCmp' /> - Use this Syntax if no namespace is defined by you.

<yourNameSpace:childComponent aura:id='childCmp' /> Use this Syntax if you have your own       namespace is defined by you.

Step2: - Create a button OR any event in which you want to execute the child controller method.

<lightning:button variant="brand" label="Submit" onclick="{! c.handleClick }" />

Step3 : - Call the child controller method from the parent controller method.

({

handleClick : function(component, event, helper){

// Find the child component using the aura:id that we have given while creating the parent component and store the same into a variable.

var childCmp = component.find('childCmp');

// Call the Child Controller method using childCmp variable dot method name defined into the child component

childCmp.sampleMethod('Sample Value for Param 1', 'Sample Value For Param 2'); // Pass the parameters here

}

})

Example: - For an example we will take a very simple scenario for creating quick contact for the selected account doing this we will reduce the work of going to account detail page and then create a contact from there. 

![Aura Method](https://github.com/amitastreait/Aur-Method-in-Lightning-Component/blob/master/Parent%20-%20Child/Aura%20Method.gif)
