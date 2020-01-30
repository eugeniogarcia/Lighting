# Usefull commands

Create a project:

```sh
sfdx force:project:create -n xxxxxxx
```

Create a Scratch Orgs:

```sh
sfdx force:org:create -f config/project-scratch-def.json -a cap6
```

Generate a password for the Scratch Org:

```sh
sfdx force:user:password:generate -u cap6
```

Open the Scratch Org:

```sh
sfdx force:org:open -u cap6
```

Look at the details of the Scratch Org:

```sh
sfdx force:org:display -u cap6
```

## Fetching metadata from non-DX

```sh
sfdx force:source:retrieve --metadata AppMenu:AppSwitcher
```

## Deploying to the non-DX org

We need to conver to the metadata formata to create the package we need to publish. First we convert it:

```sh
sfdx force:source:convert -d mdapi_output_dir -n "Capitulo 6"
```

Now we deploy it:

```sh
sfdx force:mdapi:deploy --deploydir mdapi_output_dir -u egsmartin@gmail.com -w 3
```

## Logs

Stream the logs on the local console:

```sh
sfdx force:apex:log:tail --color
```
