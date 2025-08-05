# E-Voting System Backend

A secure e-voting system backend implemented in C++ using **Merkle Trees** and **Hash Chains** for vote integrity and verification.

## Features

- ✅ **Merkle Tree Implementation** - For efficient vote verification
- ✅ **Hash Chain (Blockchain-like)** - For tamper-evident vote storage
- ✅ **SHA-256 Hashing** - For cryptographic security
- ✅ **Vote Verification** - Real-time vote verification system
- ✅ **Election Results** - Live election result tracking
- ✅ **Duplicate Vote Prevention** - Prevents double voting

## Architecture

### Data Structures

1. **Vote Structure**
   - Voter ID, Name, Email
   - Constituency and Candidate
   - Timestamp and Vote Hash
   - Previous Hash (for chain linking)

2. **Merkle Tree**
   - Binary tree of vote hashes
   - Efficient verification of vote integrity
   - Single root hash represents all votes

3. **Hash Chain**
   - Blockchain-like structure
   - Each block contains vote hash and previous block hash
   - Proof of work (4 leading zeros)
   - Tamper-evident design

## Dependencies

- **OpenSSL** - For SHA-256 hashing
- **nlohmann/json** - For JSON handling
- **C++17** - Modern C++ features

## Installation

### Prerequisites

```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install build-essential cmake libssl-dev nlohmann-json3-dev

# CentOS/RHEL
sudo yum install gcc-c++ cmake openssl-devel

# macOS
brew install cmake openssl nlohmann-json
```

### Building

```bash
cd backend
mkdir build
cd build
cmake ..
make
```

### Running

```bash
./voting_system
```

## API Functions

### 1. Submit Vote
```cpp
bool submitVote(voterId, voterName, voterEmail, constituency, candidate)
```
- Validates voter hasn't voted before
- Generates vote hash
- Adds to hash chain
- Rebuilds Merkle tree

### 2. Verify Vote
```cpp
json verifyVote(voterId)
```
- Checks if vote exists
- Validates vote hash
- Verifies presence in hash chain
- Returns detailed verification result

### 3. Get Election Results
```cpp
json getElectionResults()
```
- Returns total vote count
- Shows votes per candidate
- JSON formatted output

### 4. Get System Status
```cpp
json getSystemStatus()
```
- Total votes cast
- Hash chain length
- Merkle root hash
- Last block hash

## Security Features

### 1. Cryptographic Hashing
- SHA-256 for vote hashing
- Unique hash for each vote
- Tamper detection

### 2. Hash Chain
- Each block linked to previous
- Proof of work (4 leading zeros)
- Immutable vote history

### 3. Merkle Tree
- Efficient vote verification
- Single root represents all votes
- Quick integrity checking

### 4. Duplicate Prevention
- Voter ID tracking
- Prevents double voting
- Real-time validation

## Example Usage

```cpp
EVotingSystem votingSystem;

// Submit a vote
votingSystem.submitVote("VOTER001", "John Doe", "john@email.com", 
                       "North Delhi", "candidate1");

// Verify a vote
json result = votingSystem.verifyVote("VOTER001");
std::cout << result.dump(2) << std::endl;

// Get results
json results = votingSystem.getElectionResults();
std::cout << results.dump(2) << std::endl;
```

## Output Example

```
=== E-Voting System Backend ===
Vote submitted successfully for voter: VOTER001
Vote Hash: a1b2c3d4e5f6...
Block Hash: 0000f8a7b9c2...

System Status: {
  "totalVotes": 4,
  "hashChainLength": 4,
  "merkleRootHash": "abc123...",
  "lastBlockHash": "0000f8a7b9c2..."
}

Election Results: {
  "totalVotes": 4,
  "candidates": {
    "candidate1": 2,
    "candidate2": 1,
    "candidate3": 1
  }
}
```

## Integration with Frontend

The backend can be integrated with the HTML/CSS/JS frontend using:

1. **CGI (Common Gateway Interface)**
2. **HTTP Server** (using libraries like Crow or Pistache)
3. **WebSocket** for real-time updates

## Future Enhancements

- [ ] Database integration (SQLite/PostgreSQL)
- [ ] REST API endpoints
- [ ] WebSocket support
- [ ] Admin panel
- [ ] Vote encryption
- [ ] Multi-constituency support
- [ ] Audit logging
- [ ] Performance optimization

## License

This project is for educational purposes. Use responsibly in production environments. 