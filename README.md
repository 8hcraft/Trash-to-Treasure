# Trash-to-Treasure
Low brs gotchis utility

# **Aavegotchi Pity Poker: The Whales' Playground**  
*A High-Revenue Poker Variant for Weak Gotchis & Whale Entertainment*  

---

## **1. Concept Overview**  
**Core Idea**:  
A **rigged poker table** where:  
- **Weak Gotchis (40-60 traits)** are allowed to play.  
- **Whales (top 10%)** get matched against them for easy wins.  
- **DAO takes a rake** while compensating weak Gotchi owners.  

**Why It Works**:  
- Weak Gotchis finally have **utility**.  
- Whales get **low-risk, high-reward games**.  
- DAO earns **consistent fees** from every table.  

---

## **2. Game Rules (Rigged Fairness)**  

### **A. Table Mechanics**  
| Rule                      | Weak Gotchi Player          | Whale Player               |  
|---------------------------|----------------------------|----------------------------|  
| **Win Rate**              | 30% (rigged)               | 70% (rigged)              |  
| **Entry Fee**             | 2 GHST                     | 10 GHST                    |  
| **Payout**                | 3 GHST if they win         | 12 GHST if they win        |  
| **DAO Cut**               | 1 GHST per hand            | 3 GHST per hand            |  

### **B. Gotchi-Based Advantages**  
- **Weak Gotchi Bonus**: If all traits are between 45-55 → **+5% win chance**.  
- **Whale Bonus**: For every 10k GHST staked → **+1% win chance** (capped at 80%).  

---

## **3. Smart Contract Implementation**  

### **Key Functions**  
**1. Rigged Hand Determination**  
```solidity  
function determineWinner(address weakPlayer, address whalePlayer) internal returns (address) {  
    uint256 whaleWinRate = 70;  
    whaleWinRate += (ghstStaked[whalePlayer] / 10_000); // +1% per 10k GHST staked  
    whaleWinRate = min(whaleWinRate, 80); // Cap at 80%  

    uint256 rand = uint256(keccak256(abi.encodePacked(block.prevrandao, weakPlayer))) % 100;  
    return (rand < whaleWinRate) ? whalePlayer : weakPlayer;  
}  
```  

**2. Fee Distribution**  
```solidity  
function distributeWinnings(address winner, bool isWhale) internal {  
    uint256 daoCut = isWhale ? 3 ether : 1 ether;  
    uint256 playerPrize = isWhale ? 12 ether : 3 ether;  

    payable(DAO_TREASURY).transfer(daoCut);  
    payable(winner).transfer(playerPrize);  
}  
```  

---

## **4. Revenue Projections**  
*(Based on 100 daily games)*  

| Scenario                | Daily DAO Revenue | Monthly DAO Revenue |  
|-------------------------|-------------------|---------------------|  
| **10 Whales + 50 Weak** | 200 GHST          | 6,000 GHST          |  
| **50 Whales + 200 Weak**| 800 GHST          | 24,000 GHST         |  

---

## **5. Player Incentives**  

### **For Weak Gotchi Owners**  
- **"Nothing to Lose"**: Only 2 GHST to enter, chance to win 3 GHST.  
- **Passive Income**: Can rent Gotchis to whales for **1 GHST/hour**.  

### **For Whales**  
- **Guaranteed Profit**: 70-80% win rate → easy GHST farming.  
- **Status Symbols**: "Pity Crusher" leaderboards & wearables.  

---

## **6. Launch Roadmap**  
1. **Week 1**: Deploy smart contracts on Base.  
2. **Week 2**: Open beta for top 100 Gotchi holders.  
3. **Month 1**: Full launch with UI at **pity.aavegotchi.com**.  as an example.

Every number of costs os TBD by DAO.
