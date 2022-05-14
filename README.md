# Klaybank Proposal

## Proposal
1. Make proposal PR
2. Get reviews and approvals
3. Upload proposal to ipfs

## IPFS
1. Sign up for [pinata](https://pinata.cloud).
2. Get API Key and Secret Key
3. Get a raw copay of the proposal file from Github. E.g. https://raw.githubusercontent.com/klaybank/proposal/main/content/proposal-1.md
4. Set .env in the root directory (`./proposal`)
   ```text
    FILE_PATH=
    TITLE=
    SHORT_DESCRIPTION=
    PINATA_KEY=
    PINATA_SECRET=
    ```
5. Upload using the below command
    ```text
    npm i && npm run upload
    ```
