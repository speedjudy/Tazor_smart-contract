

1. deploy Authority.sol first with 4 constructor params : deployer's address.
2. deploy TAZOR.sol.   	with deployed authority's address
3. deploy TAZ.sol.	with deployed authority's address		// same as tazor but totalsupply
4. deploy treasury
	[testnet]									BSC testnet  								BSC mainnet
		dai:	0x8a9424745056Eb399FD19a0EC26A14316684e274						0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3
		usdt: 	0x7ef95a0FEE0Dd31b22626fA2e10Ee6A223F8a684						0x55d398326f99059fF775485246999027B3197955
		usdc:	0xeb8f08a975Ab53E34D8a0330E0D34de942C95926
		busd:	0x78867BbEeF44f2326bF8DDd1941a4439382EF2A7						0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56

			0x0000000000000000000000000000000000000000


	deposit function is called from bondDepository.
	

5. deploy staking.

5.5 deploy staking helper 	// bond contact with staking contract via stake helper.
				// need to update to stakeTAzor()

	//6. deploy distributor	// why is this needed?

	//7. deploy DAO.		// singleton:

8. bonding calculator		// 

8. deploy bonddepository 	// set dao address ad owner's wallet address.  





============================		BSC TEST

				0x0000000000000000000000000000000000000000



Test case

1. Tazor, Taz:  mint, burn  --------  ok
2. Treasury setting.
	
	/** after bonddepository created, you should done below operation.  **/
	function queue(
		Manageing 	manage			0
		address 	bondaddress		bonddepository address
	){}

	enum MANAGING { RESERVEDEPOSITOR, RESERVESPENDER, RESERVETOKEN, RESERVEMANAGER, LIQUIDITYDEPOSITOR, LIQUIDITYTOKEN, LIQUIDITYMANAGER, DEBTOR, REWARDMANAGER, STAZOR }

	function toggle(
		Managing 	manage 			0
		address		bondaddress		bonddepository address
		address		calcaddress		0x0000000000000000000000000000000000000000
	){}


	
2.5	in authority.sol pushVault(treasury address, true)  : give treasury right to mint tazor.



2.6 : should deploy bondCalculator for TAZOR : used in tazor lp bond.

	  should deploy bondCalculator for TAZ   : used in taz   lp bond.


2.9. BondDepository
	

	A. in constructor: the bondcalculator should be 	0x0000000000000000000000000000000000000000      if stable coin

	B. function initializeBondTerms(
	        uint _controlVariable, 		20
	        uint _vestingTerm,			28800			//	28800 (a day)
	        uint _minimumPrice,			100			// 	100 is 1$
	        uint _maxPayout,			1000 		//	100000 = 100%		// determin maximum bond size => ratio of bondsize : totalTazor : limitation for slippage.
	        uint _fee,					100  		//	10000 = 100%
	        uint _maxDebt,				2000000000000000	// 1000000 Tazor 9decimal
	        			
	        uint _initialDebt			500000000000000  // 
	    ){}   
   

    C. Treasury setting is needed after init the bond in tazorTreasury.sol.

    	** you can add token and lp token using queue and toggle function in treasury.

    	@  to add reserve token in the constructor.
  				queue(0, bondaddr),  toggle(0, bondaddr, 0)

    	@  to add reserve token not in the constructor. 
    						queue(2, addr),  toggle(2, addr)
    				then    queue(0, bondaddr),  toggle(0, bondaddr, 0)

    	#  to add lp token 	  queue(5, lptokenaddr)   toggle(5, lptokenaddr, calcAddr),
    				then  queue(4, lpBondAddr),  toggle(4, LpBondAddr, calcAddr)


    	when lp token,    initial debt is 200000000000000


    	D. We should call Queue(), then Toggle() function with Manage right.

    E. Then Approve DAI.
    F. Check treasury's vault right.


    //// *************  auto lp increase.
    call addCreateLpToken(token address, bool)    



    function deposit(
		uint _amount, 				2000000000000000000	// 2 principles
        uint _maxPrice,				30000		// 300$
        address _depositor			wallet address
    ){}


    when deposit fail. please set debt again.

    function setTotalDebt(){
    								200000000000000         //  200000 tarzor
    }


    function redeem(
    	address _recipient,			wallet address
    	bool	_stake				true or false
    ){}

  
2.9 : deploy redeemHelper.


3. Treasury
	In Treasury contract, 	confirm totalReserves
	In Tazor contract,		confirm balance 

4. Staking
	staking Tazor
	staking Taz
	APR
	burn
	reward

5. deploy redeemHelper.

	add bonddepository to redeemHelper.

========================== 2022/02/09 =============================

	[testnet]									BSC testnet  								BSC mainnet
		dai:	0x8a9424745056Eb399FD19a0EC26A14316684e274						0x1af3f329e8be154074d8769d1ffa4ee058b1dbc3
		usdt: 	0x7ef95a0FEE0Dd31b22626fA2e10Ee6A223F8a684						0x55d398326f99059fF775485246999027B3197955
		usdc:	0xeb8f08a975Ab53E34D8a0330E0D34de942C95926
		busd:	0x78867BbEeF44f2326bF8DDd1941a4439382EF2A7						0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56
		Tazor-dai: 	0x9D3cB6C1caBceC5cE65d68444851ad78EFdb4173
		Taz-dai:	0xFBa386ED232904F25117FD2b2c97f280EA9FDFd7
			
			0x0000000000000000000000000000000000000000

dao wallet : 		0x7b93DC0D37DcEB232DE99a08944614f0EBdeADe3

====================================================
authority: 			0xF6152F12B3BFfAF73af5c4Faaa31acF3649E3daa
tazor: 				0x9aB2B0730DFE6c44C0B9649Cc458B3A1438fbF31
taz:				0xa583B35e2C080CC85955dE58aBE44e186599b341

Treasury:			0xE2888a219a74cFDfcF93214a18DA6a0a126a0757
Staking: 			0x1842aF8FA40291585e022d881bbb15C49d9DE149
TazorBondCal: 		0x661d77B9fF1Cc4286eF476f5A21a6875926D732C
TazBondCal:			0x66abaAf86f972Dc0A30F6323F554FDF4C54Fe688
DaiBondDepo:		0xe0f1708A61D367C40cf9E7915386eCe60b75dee6
UsdtBondDepo: 		0x9d7055C91d368d7d2114039A934E134AdaE53477
BusdBondDepo:		0xC533375052F4dd7284d275Da300F228E4d002BA2
TazorDaiBondDepo:	0xfeeD31224FB75a6B2cbD2ABFf7FEf32B1752802C
TazDaiBondDepo:		0xef8DeC8451dbCC97bD13f579F8d591d69E10C23C
RedeemHelper:		0x10293825a07C53939a1b7Bb123A285C7fFd6a5e3


tazor-dai:	0xbDa71E17b312990e80ED4D9E8076EaDd2491d760
taz-dai:	0x985a94ae8BFa882117B7E6C0194B5297ED9034d1


presale:		    0x9B2E5a6340b0EF6FB093D70043fC75843aCBB82B
		1000000000000000
		100000000000000000000000
		400000000000000
		400000000000000
		1000000000000000000000000
		1000000000000000000000000


==========  auto lp increate            approve  stable 	1000000000000000000000
treasury: 			0xBD293391fdA4371cC8c26466c22506B6D55Ba541

DaibondDepository: 	0x8724041E153FDA930D15e9DA96434c7E28B75Eb4
usdtBondDepository: 0xDc4182D1a58aeB07849f08EAd5283C9AF629C8fb
busdBondDepository: 0x118F5326e9289cfC1749d775919316A080c5daAd
TazorDaiBondDepost: 0x4a88658cEB483aBfa5D9D556df8dba4D2560029a
TazDaiBondDeposit:	0x2Cf034186caF2Bb7C84971F2Bb839c19CeFB800A

addcreatelptoken(addr, bool);


0.0025
2500000000000000

======================= 11111111111111=========================
tarzan:TazorAuthority deployed Address====> 0x1A17AD5441dF88da456Dc9fDbE518a0651C77994
tarzan:tazorContract deployed Address====> 0x54e98D562265a829b40A71350e40d4Ad3a2C6fCA
tarzan:tazContract deployed Address====> 0x21A5419fA0B1352C381d86216098db13b2710d40
tarzan:stakingContract deployed Address====> 0x770C6cb76b0598cf664f7F9239a6358ef1AB22Df
tarzan:TazorAuthority pushed vault to staking address ====
tarzan:TazorTreasury deployed Address====> 0x51725F7e28a7AC88D9Ba5BC940400C23A0beAa8c
tarzan:TazorAuthority pushed vault to treasyrt address ====>
tarzan:DAIbondDepository deployed Address====> 0xF16384ce46a0A05892aA7e34A841f69167c02a01
tarzan:Initialize DaiBondDepository====>
tarzan:Queue set in DaiBondDepository====>
tarzan:Toggle set in DaiBondDepository====>
tarzan:USDTbondDepository deployed Address====> 0x5b0FaA2c9605E7a08990bA213E82654d92441109
tarzan:Initialize usdtBondDepository====>
tarzan:Queue, Toggle set in USDTBondDepository====>
tarzan:BUSDbondDepository deployed Address====> 0xAb49074D66264dB7a82A260fA52160a099f4215A
tarzan:Initialize busdBondDepository====>
tarzan:Queue, Toggle set in BUSDBondDepository====>
tarzan:redeemhelper deployed Address====> 0x5d6E96a5b7e524820799f27218A158F4AB62F3Ea
tarzan:redeemhelper add bond Address====>
tarzan:TazorPreSale deployed Address====> 0xe2710EFE1391bd37e77769625fFE4b04A6e14967
tarzan:current blocknumber====> 17779052

tazor-dai: 0xdcB43ecB329459653B5372B6b16a8eE4343a085E
taz-dai:   0xA5b5716E740a275bEf3F1E8e16CE60a80dda2C3b


change lp token address in all bonds
taz-dai.
taz-dai-token.



*******   when making liquidity please add it with tazor above option      dai   below option.

test router address
0x7e3411b04766089cfaa52db688855356a12f05d1



================  avalanche ============
const _ZERO = "0x0000000000000000000000000000000000000000";

const _ACAKE = "0x2542250239e4800B89e47A813cD2B478822b2385";
const _AUSDT = "0x5F1a9A617eF90815049D564954Fd634AB54d02E6";
const _ADOT =  "0xaA4a71E82dB082b9B16d4df90b0443D83941BEC4";
WAVAX: 		0xd00ae08403B9bbb9124bB305C09058E32C39A48c


authority 	0x1355df8cF7Be962D3a26895Cc4f821EAbcdF9969
tazor     	0x784fE7511E5CE3a55f52CA1FeFA7d45D2B06E1FB
taz 		0x81186E77c327b7D55Ca740Cd99B047e03a79946E
staking 	0x9A841bfB84a11a44B10906D79FdDfC873A407461

presale:	0x68F561c8c92F746018c42445d1a5D9D653813c60			please change slippage from 150 to 110 later.

treasury    0xcC7d6585F58Fb5cd64CfB1315e4Bcf347909a102


acakeBond:	0xcF48B499475E0346ff34Ee55F1998316eC6C4929
ausdtBond:	0x5D5E53C23819D1504288bBCcA15c4520f085fba8



tazor-avax: 0x08e3A3b0cD19fD8Fe515934f1877456Ebe9F3f03
taz-avax:   0x24c289Aa4ef278b49a0d6B4da8aAEDa267cb247c
usdt-avax: 	0xe657DcD108B440845B27C15AED878f20b40D8b3F




deploy treasury.
push vault to treasury
add tokens to treasury for auto bonding.

deploy bonding contract.
inititalize bonding.
treasury queue.
treuasury toggle.





********   for calling swapExactTokenforETH () we should make calling function payable  and    add following code.
	receive() payable external {}



































===============  FrontEnd modification.

DAI	USDT 	DOT

*** set 	tazor_native_token/ taz_native_token: 	avalanche testnet
	bondaddress: addrss of usdt-avax		// needed for calculating avax price.
	reserveaddress: tazor-avax, taz-avax.




later modify:
	helper/index/getTazMarketCap, getTazMarketPrice
	src/lib/bond.ts
		getLpTokenAssetNum  ==> change decimal for usdt.






