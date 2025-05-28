Understanding how the gas fee mechanism works is crucial for optimizing transactions and managing costs effectively. Badly designed DApps can be at the mercy of network congestion, for example, when gas prices surge as smart contracts compete to have their transactions processed sooner.

Optimizing Solidity code for gas efficiency can be a complex and time-consuming process. It requires a deep understanding of the EVM and its execution model. Workarounds include the use of wallets that allow you to customize the gas price, the choice of off-peak times when fees are lower and the use of Layer 2 solutions that handle transactions off-chain. 

Solidity requires developers to clearly define the data type of each variable and method. It allows for flexible code by supporting different types of polymorphism, in other words, ways to use the same code for different data types. While Solidity tries to ensure type safety by automatically handling some conversions, it will flag errors for potentially unsafe conversions. 

For advanced operations like interacting directly with the computer's memory, Solidity provides tools that give the developer more control, but also more responsibility. Solidity supports code reusability through features like multiple inheritance and importing external files, which makes it easier to build complex contracts by combining existing components. 

This can be both a blessing and a burden. Some developers may not fully understand the code they are reusing. For example, it’s possible to fork the entire source code of Uniswap, the most popular DEX on Ethereum. 

Over the years, Solidity's design has made it vulnerable to all sorts of security exploits. Reentrancy attacks, integer overflows/underflows, sandwich attacks and logic errors all feature in well documented hacks. While the Ethereum ecosystem has responded by developing tools and best practices to mitigate risks, a large onus remains on the developer to write secure code. 

Formal verification is used to mathematically prove the correctness and security of contracts. But these tools are not stress tested or mature enough for complex Solidity contracts, and this increases the risk of undiscovered bugs. 

Some developers find Solidity code to be overly verbose. Compared to other languages, it requires more lines of code to achieve the same functionality. This can affect readability and maintainability, especially for larger projects. 

Solidity lacks certain high-level abstractions and features found in more modern languages. This can make it challenging to express complex logic or implement sophisticated data structures efficiently. 

It is not uncommon for Solidity code to have unintended side effects that often result in hacks and financial loss. None more so than in the infamous 2016 DAO hack. 

After reviewing the DAO hack, a researcher at Cornell University stated that Solidity was partially to blame: *‘this was actually not a flaw or exploit in the DAO contract itself: technically the Ethereum Virtual Machine (EVM) was operating as intended, but Solidity was introducing security flaws into contracts that were not only missed by the community, but missed by the designers of the language themselves.’* 

Another key difference is that Ethereum requires you to pay Gas for failed contract executions. For example, if there is a check and a user’s NFT validates to **False**, the contract ends early but still costs the gas consumed until that validation point. On Cardano, you need to provide the UTxO with the asset as an input, but if this evaluates to **False**, there is no fee.

Back to our restaurant analogy. If you are paying your bill with the account-based model, you do not have certainty that the transaction will execute as expected. You are dependent on the global state and network activity. You may be at the front of the queue in your local restaurant about to pay for your dinner, but the machine may be busy dealing with a man on the other side of the world paying for his breakfast. After waiting patiently, your transaction fee may now be larger than when you originally got the bill.
