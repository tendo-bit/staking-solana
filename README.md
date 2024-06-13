# Solana-staking

1. Program Deployment
    - Anchor build & deploy & upgrade
    - Anchor project build: anchor build
    - Anchor project deploy: anchor deploy
    - Anchor project upgrade: anchor upgrade --program-id "programID" "so file path"

    *** Ex: anchor upgrade --program-id 3CoU3M7s8zMQzt3mS6rex11xKBgBd4P58Efk11TZuvct ./target/deploy/wmp_staking.so ***
    
    (.so file is created after anchor build)

2. Program initialization
   - yarn migrate:init-devnet
   - yarn migrate:init-mainnet

3. Token deploy
   - yarn deploy:token-devnet
   - yarn deploy:token-mainnet

4. Create pool for each farm or pool
   1) Should set some parameters before create pool in create-stake-pool.ts file

      - Replace Stake and reward token addresses     
      - Fee percentage
      - Reward per second

   2) yarn migrate:create-pool-devnet
   3) yarn migrate:create-pool-mainnet

    ** After create pool, you should save pool address **
5. Test dapp
  - Update addresses in state.ts file
    Confirm Stake token and reward token, pool address, rpc 
  - Update owner address in accounts.ts file (in getStakeAccounts() method)

  - Run: yarn start:dev

    Can get Escrow address after you stake token

   *** Should send reward token to Escrow address to check “get reward” ***


*** Common errors ***
 - When program upgrade  Error: "No more space for program…."
    solana program extend <PROGRAM_ID> <ADDITIONAL_BYTES>
 - Resuming failed transaction
    solana-keygen recover -o <KEYPAIR_PATH>
    solana program deploy --buffer <KEYPAIR_PATH> <PROGRAM_FILEPATH>

    https://solana.stackexchange.com/questions/5961/how-to-resume-a-deploy