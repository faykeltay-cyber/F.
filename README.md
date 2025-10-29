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
plt.show()

