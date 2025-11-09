# F.

# IRT Cipher Cash Flow Map (Hybrid: Cipher + Cash Flow)
# Author: Felicia Ann Kelley System Model
# Version: 1.0

import hashlib
import networkx as nx
import matplotlib.pyplot as plt

# === CONFIGURATION ===
GENESIS_TXID = "b6f6991d02d64f9f7f8b5d3c6c30f8b8e5f5d5f1e2c3c31d03c4f1cde9d9c5f1"
CHANNELS = [7, 8, 9, 10, 11]

# === FUNCTIONS ===

def derive_channel_hash(txid, channel):
    """Derive ciphered channel node hash"""
    seed = f"{txid}-{channel}".encode()
    return hashlib.sha256(seed).hexdigest()[:16]  # 16-char node id

def cipher_value(channel_hash):
    """Convert hash to numeric signature (symbolic key)"""
    val = int(channel_hash, 16)
    return round((val % 65535) / 256, 4)

def cash_flow_function(channel):
    """Assign symbolic cash flow to each channel"""
    flows = {
        7: "AI Microtool Sales",
        8: "Affiliate Revenue",
        9: "Digital Asset Sales",
        10: "Crypto Yield / Staking",
        11: "Reinvestment Engine"
    }
    return flows.get(channel, "Undefined")

# === BUILD GRAPH ===
G = nx.DiGraph()

# Genesis root
G.add_node("GENESIS_TXID", layer="root", color="#00FFFF", label="Genesis Seed")

# Build channels
for ch in CHANNELS:
    ch_hash = derive_channel_hash(GENESIS_TXID, ch)
    symbol = cipher_value(ch_hash)
    flow = cash_flow_function(ch)
    node_name = f"CH_{ch}"
    G.add_node(node_name, layer="channel", color="#00FFFF", label=f"{flow}\nCipher:{symbol}")
    G.add_edge("GENESIS_TXID", node_name)

# Yield node (aggregates outputs)
G.add_node("YIELD_NODE", layer="aggregator", color="#FFD700", label="Yield / Visual Output")
for ch in CHANNELS:
    G.add_edge(f"CH_{ch}", "YIELD_NODE")

# === VISUALIZE ===
pos = nx.spring_layout(G, seed=42)
colors = [G.nodes[n]['color'] for n in G.nodes()]
labels = {n: G.nodes[n]['label'] for n in G.nodes()]

plt.figure(figsize=(9, 6))
nx.draw(G, pos, with_labels=True, node_color=colors, node_size=2600,
        font_size=9, font_color='black', font_weight='bold', edgecolors='black')
nx.draw_networkx_labels(G, pos, labels=labels, font_size=8)
plt.title("IRT Cipher Cash Flow Structural Map", fontsize=13, fontweight='bold')
plt.axis('off')
plt.show(# Develop with Coinbase

export default function BuildWithCoinbase() {
  const [active, setActive] = useState("onchain");
  const cards = [{
    id: "onchain",
    title: "Build onchain",
    description: "Dev-first frameworks."
  }, {
    id: "programmatic",
    title: "Need integrations?",
    description: "Connect Coinbase apps."
  }, {
    id: "institutional",
    title: "For institutions",
    description: "Enterprise trading tools."
  }];
  const cloneCmd = "git clone --depth=1 https://github.com/coinbase/cdp-sdk && cd cdp-sdk/examples/typescript/quickstart";
  const startCmd = "npm install && npm run build && npm start";
  return <>
      <style jsx global>{`
        /* Remove extra margins from What next cards */
        .what-next-grid > a {
          margin-top: 0 !important;
          margin-bottom: 0 !important;
        }
        .what-next-grid > a > div {
          margin-top: 0 !important;
          margin-bottom: 0 !important;
        }
        /* Reduce Steps component bottom margin */
        .mintlify-steps {
          margin-bottom: 1.5rem !important;
        }
        /* Ensure consistent card height */
        .tab-cards > div > div {
          height: 100%;
        }
      `}</style>
      
      <div className="not-prose grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 w-full mb-10 tab-cards">
        {cards.map(({id, title, description}) => {
    const isActive = active === id;
    const iconName = id === "onchain" ? "code" : id === "programmatic" ? "plug" : "building-columns";
    return <div key={id} onClick={() => setActive(id)} className="relative cursor-pointer flex">
              <div className={`
                  flex-1 flex flex-col p-6 rounded-lg border transition-all duration-200
                  ${isActive ? "border-blue-500 bg-blue-50/50 dark:bg-blue-950/10" : "border-gray-200 dark:border-gray-800 hover:border-gray-300 dark:hover:border-gray-600"}
                `}>
                <div className="flex items-center gap-3 mb-3">
                  <Icon icon={iconName} className="text-blue-600" />
                  <h3 className="font-semibold text-base">{title}</h3>
                </div>
                <p className="text-sm text-gray-600 dark:text-gray-400">{description}</p>
              </div>
            </div>;
  })}
      </div>

      {active === "onchain" && <>
          <Heading level={2} id="send-your-first-request">Send your first onchain request</Heading>

          <Warning>
            Download your API key when prompted! It's only shown once. For production use, do not download key files. Instead, use environment variables.
          </Warning>

          <Steps titleSize="p">
            <Step title="Get your API credentials">
              Sign up at{" "}
              <a href="https://portal.cdp.coinbase.com" target="_blank" rel="noreferrer">
                portal.cdp.coinbase.com
              </a>
              , then navigate to{" "}
              <a href="https://portal.cdp.coinbase.com/projects/api-keys" target="_blank" rel="noreferrer">
                API Keys
              </a>
              {" "}and{" "}
              <a href="https://portal.cdp.coinbase.com/products/server-wallets" target="_blank" rel="noreferrer">
                Wallets
              </a>
              {" "}to create your Secret API key and Wallet Secret.
            </Step>

            <Step title="Clone the Quickstart repo">
              <CodeGroup>
                <CodeBlock language="bash" filename="Terminal">
                  {cloneCmd}
                </CodeBlock>
              </CodeGroup>
            </Step>

            <Step title="Run the project">
              <CodeGroup>
                <CodeBlock language="bash" filename="Terminal">
                  {startCmd}
                </CodeBlock>
              </CodeGroup>
            </Step>

            <Step title="You're done!">
              <CodeGroup>
                <CodeBlock language="bash" filename="Terminal">
{`🔐 Loaded API key from cdp_api_key.json
🔐 Loaded wallet secret from cdp_wallet_secret.txt
✅ Created EVM account: 0x1234567890123456789012345678901234567890
🚰 Received testnet ETH: 0xabcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890
📦 TX confirmed: https://sepolia.basescan.org/tx/0x1a2b3c4d5e6f7890abcdef1234567890abcdef1234567890abcdef1234567890`}
                </CodeBlock>
              </CodeGroup>
              
              <AccordionGroup>
                <Accordion title="What happened?">
                  <ol className="list-decimal list-inside space-y-3">
                    <li><strong>Authentication</strong>: Your Coinbase Developer Platform (CDP) API credentials were used to authenticate.</li>
                    
                    <li><strong>Wallet creation</strong>: An <a href="/server-wallets/v2/introduction/accounts">EVM account</a> (a blockchain address compatible with Ethereum and other EVM networks) was created on <a href="https://docs.base.org/docs/network-information#base-testnet-sepolia">Base Sepolia</a>, our <a href="/get-started/supported-networks#testnets">test network</a> for safe experimentation before mainnet deployment.</li>
                    
                    <li><strong>Request testnet funds</strong>: The app requested free testnet ETH using <a href="/faucets/introduction/">CDP Faucets</a> for transaction testing.</li>
                    
                    <li><strong>Test transaction</strong>: A transaction was broadcast and confirmed onchain. View it on the block explorer using the link provided.</li>
                  </ol>
                </Accordion>
              </AccordionGroup>
              
              <Info>
                The example shows files being loaded (which must be manually downloaded). Environment variables are recommended for better security.
              </Info>
              
              <p className="mt-4">Ready to build more? Try incorporating <a href="/server-wallets/v2/using-the-wallet-api/policies/overview">policies</a> to govern account behavior, exchange tokens using our <a href="/trade-api/welcome">Trade API</a>, or explore our <a href="/get-started/demo-apps/learn">tutorials</a>.</p>
            </Step>
          </Steps>

          <Heading level={2} id="what-next" className="mt-6">What next?</Heading>
          
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 what-next-grid">
            <Card title="Use AI Tooling" href="/get-started/use-ai-tooling" icon="sparkles">
              Build faster with AI.
            </Card>
            <Card title="API Reference" href="/api-reference/v2/introduction" icon="book-open">
              Explore all endpoints.
            </Card>
            <Card title="v2 Server Wallet" href="/server-wallets/v2/" icon="wallet">
              Multi-chain wallets.
            </Card>
            <Card title="Faucets" href="/faucets/introduction/" icon="droplet">
              Get test tokens.
            </Card>
            <Card title="Trade API" href="/trade-api/welcome" icon="arrow-right-arrow-left">
              Trade at best prices.
            </Card>
            <Card title="Learning" href="/get-started/demo-apps/learn" icon="graduation-cap">
              Tutorials and guides.
            </Card>
          </div>
        </>}

      {active === "programmatic" && <>
          <Heading level={2} id="integrate-with-coinbase">Integrate with Coinbase apps</Heading>
          
          <div className="space-y-6 mt-6">
            <Card title="Coinbase App" href="/coinbase-app/introduction/welcome" icon="mobile">
              Consumer crypto app.
            </Card>
            
            <Card title="Coinbase Wallet" href="/coinbase-wallet/introduction/" icon="wallet">
              Non-custodial wallet.
            </Card>
            
            <Card title="Coinbase Commerce" href="/commerce/introduction/" icon="credit-card">
              Accept crypto payments.
            </Card>
          </div>
        </>}

      {active === "institutional" && <>
          <Heading level={2} id="build-for-institutions">Build for institutions</Heading>
          
          <div className="space-y-6 mt-6">
            <Card title="Coinbase Exchange" href="/exchange/introduction/welcome" icon="chart-line">
              Digital asset spot trading.
            </Card>
            
            <Card title="Coinbase International Exchange" href="/international-exchange/introduction/" icon="globe">
              Global derivatives exchange.
            </Card>
            
            <Card title="Coinbase Prime" href="/prime/introduction/" icon="shield">
              Custody and financing solutions.
            </Card>
            
            <Card title="Coinbase Derivatives" href="/derivatives/introduction/" icon="chart-pie">
              Crypto derivatives trading.
            </Card>
          </div>
        </>}
    </>;
})

