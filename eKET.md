# eKET

## Solidity changes from vanilla repo

1) Register specific token for converter during creation
2) Disallow arbitrary token registrations
3) Accept name/symbol for converter, since it only supports one token

## Deployment changes

1) Update TypeScript params to match new contract
2) Fork `deploy-converter.ts` to `deploy-eket.ts`
    * Deploy in prod mode
    * Supply KET as a parameter
    * Supply name/symbol
    * Decimals to 18
    * Remove deploying ERC20
    * Add verification support for contracts

## Build system changes
   
One time setup for verification:

```
npm install --save-dev @nomicfoundation/hardhat-verify
```

## (do not) Compile Circuits

There's no need to run the `zkit` commands; the `contracts/prod` directory already has stuff that matches
`circom/build`.

## Deployment setup

New .env file with:

```
PRIVATE_KEY=private_key_without_0x_prefix
SNOWTRACE_API_KEY=your_snowtrace_api_key_here
```

Deployer used for eKET (on testnet and mainnet) is `0xe90BD47d0a00A1444c275266724B9db911CE7717`.

Commands:

```
npx hardhat run scripts/deploy-eket.ts --network avaxTest
npx hardhat run scripts/deploy-eket.ts --network avaxMain
```

## Testnet / Mainnet deployments

Using the initial transactions on a fresh key, I deployed the contracts to the same address on both chains (similar
to how $KET is deployed).

```
┌──────────────────────┬──────────────────────────────────────────────┐
│ (index)              │ Values                                       │
├──────────────────────┼──────────────────────────────────────────────┤
│ registrationVerifier │ '0x9c232b6B211A2c1D0241C2fb7ab41bDF6D26d01B' │
│ mintVerifier         │ '0x99dC1888D82a012cBd064Af2326406927032E8Dc' │
│ withdrawVerifier     │ '0xC0BE496990EE15797f58Ab95E41Bb985bcEFc667' │
│ transferVerifier     │ '0xa32998909A870A4730c7Eedd2724f6AAa59a7676' │
│ burnVerifier         │ '0xfB886ECE288eEcED0aF3d5A17B377f3BF251E5AC' │
│ babyJubJub           │ '0x2fa62e8Bd4575843FD206C6506fE0b21b33E95Ce' │
│ registrar            │ '0x06622994B42d6D98fbEe08AaBB368f8064DD593e' │
│ encryptedERC         │ '0x8C6aE98Db339fb884cF81f64FC6d18a23589Ad56' │
└──────────────────────┴──────────────────────────────────────────────┘
```
