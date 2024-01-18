# Other

## M Three Sixty Five

NOTE: This is the challenge portal that will start the deployable container environment for the "M Three Sixty Five" challenge set below.
  
There is no flag for this challenge itself.
  
Connect with SSH, with username `user` and SSH password `userpass`. Your syntax may look like: `ssh user@chal.ctf.games -p [PORTNUMBER]`
  
When you connect to the session for the very first time, you will be authenticated into a Microsoft 365 environment. WARNING: Once you disconnect, you will need to restart your container to reauthenticate** **Press the `Start` button on the top-right to begin this challenge.

### General Info

*Welcome to our hackable M365 tenant! Can you find any juicy details, like perhaps the **street address** this organization is associated with?*

### Walkthrough

Running `Get-AADIntTenantDetails` will return the details for a given tenant. In this case, this gives us the flag:

![M365 General Info - Flag](/images/m365_ge_flag.png)

```
flag{dd7bf230fde8d4836917806aff6a6b27}
```

### Conditional Access

This tenant looks to have some odd [Conditional Access Policies](https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/overview). Can you find a weird one?

### Walkthrough

Running `Get-AADIntConditionalAccessPolicies` yields the flag:

![M365 Conditional Access - Flag](/images/m365_ca_flag.png)

```
flag{d02fd5f79caa273ea535a526562fd5f7}
```
### Teams

We observed saw some sensitive information being shared over a Microsoft Teams message! Can you track it down?

### Walkthrough

Running `Get-AADIntTeamsMessages` will return the latest Teams messages and the flag:

```
> Get-ADDIntTeamsMessages | Format-Table id,content,deletiontime,*type*,DisplayName
```

![M365 Teams - Flag](/images/m365_teams_flag.png)

```
flag{f17cf5c1e2e94ddb62b98af9fbbd46e1}
```

### The President

One of the users in this environment seems to have unintentionally left some information in their account details. Can you track down The President?

### Walkthrough

First, we can run `Get-AADIntUsers` to get information about users:

```
> Get-AADIntUsers | Select UserPrincipalName,ObjectId,ImmutableId
```

![M365 The President - Users](/images/m365_tp_users.png)

Going through each user with `Get-AADIntUser` and specifying the Principal Name with the `-UserPrincipalName` option, we obtain the flag:

![M365 The President - Flag](/images/m365_tp_flag.png)

```
flag{1e67f0dd1434f2bb3fe5d645b0f9cc3}
```
