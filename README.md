# Etherfi Sync Client
The Etherfi Sync Client is a tool designed to simplify the process of accessing validator keys for Node Operators who have won auctions. The client periodically queries the graph to detect any won auctions and imports the required information for validator key password, validator public key, validator key file, and a script to import the account to prysm.

## Setup
On remote computer, make directory for sync client and curl the executable from url:  https://github.com/GadzeFinance/etherfi-sync-clientv2/releases
```shell
# create directory and go inside it
mkdir sync-client
cd sync-client

# grab the executable from github
curl -LJO https://github.com/GadzeFinance/etherfi-sync-clientv2/releases/download/v1.0.4/<file-name-specified-in-release-table>

# unpack the executable
tar -xf <file-name-specified-in-release-table>

# make a new output directory for stake bids that have been won
mkdir output

# create configuration file
touch config.json

# edit the configuration file based on the config.json from here:
# https://github.com/GadzeFinance/etherfi-sync-clientv2/blob/master/config.json
```
```json
// Example config.json
{
  "GRAPH_URL": "<Dev URL>",
  "BIDDER": "<ETH Address used in the web UI to create bids>",
  "PRIVATE_KEYS_FILE_LOCATION": "<path to private key file generated by desktop app>",
  "OUTPUT_LOCATION": "<path to the folder where you want to output >",
  "PASSWORD": "<password used when generating the keys with the desktop app>",
  "IPFS_GATEWAY": "<IPFS gateway URL>",
  "PATH_TO_VALIDATOR": "<path to the teku validator folder>"
}
```

## How to Use
> Note: Make sure to replace the placeholder values with your own information.
Run listener: `./<binary-file-unzipped>`

That's it! The Etherfi Sync Client will now automatically query the graph for any won auctions and import the necessary information for prysm.

## Development
1. Checkout into the `dev` branch
2. Create your new branch
3. Run `go mod tidy` in order to install all the packages
4. Run `make` to build the binary.
5. Execute the binary as mentioned in the "How to Use" section
6. Once you have made your changes, run `make clean`
7. Commit and push changes to your branch and submit a PR

## How to make a release
1. Checkout into the dev branch
2. Run `git pull origin dev` to make sure you have all the changes
3. Update the `tag_name` and `release_name` in `.github/workflows/makerelease.yaml` to the new version of the release
4. Commit your changes
5. Run `git push origin master`
> Note: Pushes to the master branch will trigger a release

## Good docs to read for more understanding 
- https://docs.prylabs.network/docs/how-prysm-works/validator-lifecycle
- https://docs.prylabs.network/docs/wallet/nondeterministic
