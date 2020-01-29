# Setup

## Scratch Org

Create the Scratch Org:

```sh
sfdx force:org:create -s -f config/project-scratch-def.json -a GeoAppScratch
```

## Data

Create data:

```sh
sfdx force:data:record:create -s Account -v "Name='Marriott Marquis' BillingStreet='780 Mission St' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94103' Phone='(415) 896-1600' Website='www.marriott.com'" -u test-ctespcopymgp@example.com

sfdx force:data:record:create -s Account -v "Name='Hilton Union Square' BillingStreet='333 O Farrell St' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94102' Phone='(415) 771-1400' Website='www.hilton.com'" -u test-ctespcopymgp@example.com

sfdx force:data:record:create -s Account -v "Name='Hyatt' BillingStreet='5 Embarcadero Center' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94111' Phone='(415) 788-1234' Website='www.hyatt.com'" -u test-ctespcopymgp@example.com
```

### Backup

Backup the data we have just imported:

```sh
mkdir data

sfdx force:data:tree:export -q "SELECT Name, BillingStreet, BillingCity, BillingState, BillingPostalCode, Phone, Website FROM Account WHERE BillingStreet != NULL AND BillingCity != NULL and BillingState != NULL" -d ./data -u test-ctespcopymgp@example.com
```

We can import it with:

```sh
sfdx force:data:tree:import --sobjecttreefiles ./data/Account.json -u test-ctespcopymgp@example.com
```

We can open the Scratch org as follows:

```sh
sfdx force:org:open -u test-ctespcopymgp@example.com
```

## Coding

We created a:

- Apex controller
- Several lighting components. We personalized the markup, controller and in some cases the helper
- Event - APPLICATION

We have then created on the Scratch org a `custom tab` and a `permission set`. When we pull the Scratch Org the metadata is downloaded.

## Testing

- Create a new scratch org.

```sh
sfdx force:org:create -f config/project-scratch-def.json -a GeoTestOrg
```

- Push your local source and metadata to the scratch org.

```sh
sfdx force:source:push -u GeoTestOrg
```

Assign your permission set.

```sh
sfdx force:user:permset:assign -n Geolocation -u GeoTestOrg
```

- Load your sample data into the org

```sh
sfdx force:data:tree:import -f data/Account.json -u GeoTestOrg

Reference ID  Type     ID
────────────  ───────  ──────────────────
AccountRef1   Account  0013E000019qTHuQAM
AccountRef2   Account  0013E000019qTHvQAM
AccountRef3   Account  0013E000019qTHwQAM
```

Open your org:

```sh
sfdx force:org:open -u GeoTestOrg
```

Test the Org