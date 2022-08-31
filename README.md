# evm-opcodes
Ethereum Virtual Machine Opcodes

<br />


### 0s: Stop and Arithmetic Operations

| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x00 | STOP | Halts execution | 0 |	|
| 0x01 | ADD | Addition operation | 3 | `a, b` → `a + b` |
| 0x02 | MUL | Multiplication operation | 5 | `a, b` → `a * b`	 |
| 0x03 | SUB | Subtraction operation | 3 | `a, b` → `a - b` |
| 0x04 | DIV | Integer division operation | 5 | `a, b` → `a // b` |
| 0x05 | SDIV | Signed integer | 5 | `a, b` → `a // b` |
| 0x06 | MOD | Modulo | 5 | `a, b` → `a % b` |
| 0x07 | SMOD | Signed modulo | 5 | `a, b` → `a % b` |
| 0x08 | ADDMOD | Modulo | 8 | `a, b, N` → `(a + b) % N`	|
| 0x09 | MULMOD | Modulo | 8 | `a, b, N` → `(a + b) % N` |
| 0x0a | EXP | Exponential operation | A1: EXP | `a, b` → `a ** b` |
| 0x0b | SIGNEXTEND | Extend length of two's complement signed integer | 5 | `b, x` → `SIGNEXTEND(x, b)` |

### 10s: Comparison & Bitwise Logic Operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x10 | LT | Lesser-than comparison | 3 | `a, b` → `a < b` |
| 0x11 | GT | Greater-than comparison | 3 | `a, b` → `a > b` |
| 0x12 | SLT | Signed less-than comparison | 3 | `a, b` → `a < b` |
| 0x13 | SGT | Signed greater-than comparison | 3 | `a, b` → `a > b` |
| 0x14 | EQ | Equality  comparison | 3 | `a, b` → `a == b` |
| 0x15 | ISZERO | Simple not operator | 3 | `a` → `a == 0` |
| 0x16 | AND | Bitwise AND operation | 3 | `a, b` → `a && b`	 |
| 0x17 | OR | Bitwise OR operation | 3 | `a, b` → `a || b` |
| 0x18 | XOR | Bitwise XOR operation | 3 | `a, b` → `a ^ b` |
| 0x19 | NOT | Bitwise NOT operation | 3 | `a` → `~a` |
| 0x1a | BYTE | Retrieve single byte from word | 3 | `i, x` → `(x >> (248 - i * 8)) && 0xFF` |
| 0x1b | SHL | Shift left |	3	| `shift, val` → `val << shift`	 |
| 0x1c | SHR | Shift riight | 3 | `shift, val` → `val >> shift` |
| 0x1d | SAR | … | 3 | `shift, val` → `val >> shift` |

### 20s: SHA3
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x20 | SHA3 | Compute Keccak-256 hash | [A2](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a2-sha3) | `ost, len` → `keccak256(mem[ost:ost+len])`	 |

### 30s: Environmental Information
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x30 | ADDRESS | Get address of currently executing account | 2 | `.` → `address(this)`	 |
| 0x31 | BALANCE | Get balance of the given account | [A5](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a5-balance-extcodesize-extcodehash) | `addr` → `addr.balance`	 |
| 0x32 | ORIGIN | Get execution origination address | 2 | `.` → `tx.origin`	|
| 0x33 | CALLER | Get caller address. This is the address of the account that is directly responsible for this execution | 2 | `.` → `msg.sender` |
| 0x34 | CALLVALUE | Get deposited value by the instruction/transaction responsible for this execution | 2 | `.` → `msg.value` |
| 0x35 | CALLDATALOAD | Get input data of current environment | 3 | `idx` → `msg.data[idx:idx+32]` |
| 0x36 | CALLDATASIZE | Get size of input data in current environment | 2 | `.` → `len(msg.data)` |
| 0x37 | CALLDATACOPY | Copy input data in current environment to memory This pertains to the input data passed with the message call instruction or transaction | A3 | `dstOst, ost, len` → `.` |
| 0x38 | CODESIZE | Get size of code running in current environment | 2 | `.` → `len()this.code` |
| 0x39 | CODECOPY | Copy code running in current environment to memory | [A3](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a3-copy-operations) | `dstOst, ost, len` → `.` |
| 0x3a | GASPRICE | Get price of gas in current environment | 2 | `.` → `tx.gasprice` |
| 0x3b | EXTCODESIZE | Get size of an account's code | [A5](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a5-balance-extcodesize-extcodehash) | `addr` → `len(addr.code)` |
| 0x3c | EXTCODECOPY | Copy an account's code to memory | [A4](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a4-extcodecopy) | `addr, dstOst, ost, len` → `.` |
| 0x3d | RETURNDATASIZE | Get size of returned data from last external call, in bytes | 2 |	`.` → `size` |
| 0x3e | RETURNDATACOPY | Copy returned data from last external call | [A3](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a3-copy-operations) | `dstOst, ost, len` → `.` |
| 0x3f | EXTCODEHASH | | [A5](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a5-balance-extcodesize-extcodehash) | `address` → `hash` |

### 40s: Block Information
| Opcode | Name | Description | Gas  | Reference |
| :--- | :--- | :--- | :--- | :--- |
| 0x40 | BLOCKHASH | Get the hash of one of the 256 most recent complete blocks | 20 | `blockNum` → `blockHash(blockNum)` |
| 0x41 | COINBASE | Get the block's beneficiary address | 2 | `.` → `block.coinbase` |
| 0x42 | TIMESTAMP | Get the block's timestamp | 2 | `.` → `block.timestamp` |
| 0x43 | NUMBER | Get the block's number | 2 | `.` → `block.number` |
| 0x44 | DIFFICULTY | Get the block's difficulty | 2 | `.` → `block.difficulty` |
| 0x45 | GASLIMIT | Get the block's gas limit | 2 | `.` → `block.gaslimit` |
| 0x46 | CHAINID | Push current chain id onto stack	| 2 | `.` → `block.chain_id` |
| 0x47 | SELFBALANCE | Get balance of executing contract, in wei | 5 | `.` → `address(this).balance` |
| 0x48 | BASEFEE | | 2 | `.` → `block.basefee`  |

### 50s Stack, Memory, Storage and Flow Operations
| Opcode | Name | Description | Gas  | Reference |
| :--- | :--- | :--- | :--- | :--- |
| 0x50 | POP | Remove item from stack | 2 | `_anon` → `.` |
| 0x51 | MLOAD | Load word from memory | 3 | `ost` → `mem[ost:ost+32]`	 |
| 0x52 | MSTORE | Save word to memory | 3 | `ost, val` → `.` |
| 0x53 | MSTORE8 | Save byte to memory | 3 | `ost, val` → `.` |
| 0x54 | SLOAD | Load word from storage | [A6](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a6-sload) | `key` → `storage[key]` |
| 0x55 | SSTORE | Save word to storage | [A7](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a7-sstore) | `key, val` → `.` |
| 0x56 | JUMP | Alter the program counter | 8 | `dst` → `.` |
| 0x57 | JUMPI | Conditionally alter the program counter | 10 | `dst, condition` → `.` |
| 0x58 | PC | Get the value of the program counter prior to the increment | 2 | `.` → `$pc` |
| 0x59 | MSIZE | Get the size of active memory in bytes | 2 | `.` → `len(mem)` |
| 0x5a | GAS | Get the amount of available gas, including the corresponding reduction | 2 | `.` → `gasRemaining` |
| 0x5b | JUMPDEST | Mark a valid destination for jumps | 1 | |

### 60s & 70s: Push Operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x60 | PUSH1 | Place 1 byte item on stack | 3 | `.` → `uint8` |
| 0x61 | PUSH2 | Place 2-byte item on stack | 3 | `.` → `uint16` |
| 0x62 | PUSH3 | Place 3-byte item on stack	|	3 | `.` → `uint24` |
| 0x63 | PUSH4 | Place 4-byte item on stack	|	3 | `.` → `uint32` |
| 0x64 | PUSH5 | Place 5-byte item on stack	|	3 | `.` → `uint40` |
| 0x65 | PUSH6 | Place 6-byte item on stack	|	3 | `.` → `uint48` |
| 0x66 | PUSH7 | Place 7-byte item on stack	|	3 | `.` → `uint56` |
| 0x67 | PUSH8 | Place 8-byte item on stack	|	3 | `.` → `uint64` |
| 0x68 | PUSH9 | Place 9-byte item on stack	|	3 | `.` → `uint72` |
| 0x69 | PUSH10 |	Place 10-byte item on stack	|	3 | `.` → `uint80` |
| 0x6a | PUSH11 |	Place 11-byte item on stack	|	3 | `.` → `uint88` |
| 0x6b | PUSH12 |	Place 12-byte item on stack	|	3 | `.` → `uint96` |
| 0x6c | PUSH13 |	Place 13-byte item on stack	|	3 | `.` → `uint104` |
| 0x6d | PUSH14 |	Place 14-byte item on stack	|	3 | `.` → `uint112` |
| 0x6e | PUSH15 |	Place 15-byte item on stack	|	3 | `.` → `uint120` |
| 0x6f | PUSH16 |	Place 16-byte item on stack	|	3 | `.` → `uint128` |
| 0x70 | PUSH17 |	Place 17-byte item on stack	|	3 | `.` → `uint136` |
| 0x71 | PUSH18 |	Place 18-byte item on stack	|	3 | `.` → `uint144` |
| 0x72 | PUSH19 |	Place 19-byte item on stack	|	3 | `.` → `uint152` |
| 0x73 | PUSH20 |	Place 20-byte item on stack	|	3 | `.` → `uint160` |
| 0x74 | PUSH21 |	Place 21-byte item on stack	|	3 | `.` → `uint168` |
| 0x75 | PUSH22 |	Place 22-byte item on stack	|	3 | `.` → `uint176` |
| 0x76 | PUSH23 |	Place 23-byte item on stack	|	3 | `.` → `uint184` |
| 0x77 | PUSH24 |	Place 24-byte item on stack	|	3 | `.` → `uint192` |
| 0x78 | PUSH25 |	Place 25-byte item on stack	|	3 | `.` → `uint200` |
| 0x79 | PUSH26 |	Place 26-byte item on stack	|	3 | `.` → `uint208` |
| 0x7a | PUSH27 |	Place 27-byte item on stack	|	3 | `.` → `uint216` |
| 0x7b | PUSH28 |	Place 28-byte item on stack	|	3 | `.` → `uint224` |
| 0x7c | PUSH29 |	Place 29-byte item on stack	|	3 | `.` → `uint232` |
| 0x7d | PUSH30 |	Place 30-byte item on stack	|	3 | `.` → `uint240` |
| 0x7e | PUSH31 |	Place 31-byte item on stack	|	3 | `.` → `uint248` |
| 0x7f | PUSH32 | Place 32-byte item on stack | 3 | `.` → `uint256` |

### 80s: Duplication Operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x80 | DUP1 | Duplicate 1st stack item | 3 | `a` → `a, a` |
| 0x81 | DUP2 | Duplicate 2nd stack item | 3 | `_, a` → `a, _, a` |
| 0x82 | DUP3 |	Duplicate 3rd stack item | 3 | `_, _, a` → `a, _, _, a` |
| 0x83 | DUP4 |	Duplicate 4th stack item | 3 | `_, _, _, a` → `a, _, _, _, a` |
| 0x84 | DUP5 |	Duplicate 5th stack item | 3 | `..., a` → `a, ..., a` |
| 0x85 | DUP6 |	Duplicate 6th stack item | 3 | `..., a` → `a, ..., a` |
| 0x86 | DUP7 |	Duplicate 7th stack item | 3 | `..., a` → `a, ..., a` |
| 0x87 | DUP8 |	Duplicate 8th stack item | 3 | `..., a` → `a, ..., a` |
| 0x88 | DUP9 |	Duplicate 9th stack item | 3 | `..., a` → `a, ..., a` |
| 0x89 | DUP10 | Duplicate 10th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8a | DUP11 | Duplicate 11th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8b | DUP12 | Duplicate 12th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8c | DUP13 | Duplicate 13th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8d | DUP14 | Duplicate 14th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8e | DUP15 | Duplicate 15th stack item	| 3 | `..., a` → `a, ..., a` |
| 0x8f | DUP16 | Duplicate 16th stack item | 3 | `..., a` → `a, ..., a` |

### 90s: Exchange Operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0x90 | SWAP1 | Exchange 1st and 2nd stack items	| 3 | `a, b` → `b, a` |
| 0x91 | SWAP2 | Exchange 1st and 3rd stack items	| 3 | `a, _, b` → `b, _, a` |
| 0x92 | SWAP3 | Exchange 1st and 4th stack items	| 3 | `a, _, _, b` → `b, _, _, a` |
| 0x93 | SWAP4 | Exchange 1st and 5th stack items	| 3 | `a, _, _, _, b` → `b, _, _, _, a` |
| 0x94 | SWAP5 | Exchange 1st and 6th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x95 | SWAP6 | Exchange 1st and 7th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x96 | SWAP7 | Exchange 1st and 8th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x97 | SWAP8 | Exchange 1st and 9th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x98 | SWAP9 | Exchange 1st and 10th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x99 | SWAP10 |	Exchange 1st and 11th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9a | SWAP11 |	Exchange 1st and 12th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9b | SWAP12 |	Exchange 1st and 13th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9c | SWAP13 |	Exchange 1st and 14th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9d | SWAP14 |	Exchange 1st and 15th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9e | SWAP15 |	Exchange 1st and 16th stack items	| 3 | `a, ..., b` → `b, ..., a` |
| 0x9f | SWAP16 |	Exchange 1st and 17th stack items	| 3 | `a, ..., b` → `b, ..., a` |

### a0s: Logging Operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0xa0 | LOG0 | Append log record with no topics | [A8](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a8-log-operations) | `ost, len` → `.` |
| 0xa1 | LOG1 | Append log record with one topic | [A8](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a8-log-operations) | `ost, len, topic0` → `.` |
| 0xa2 | LOG2 | Append log record with two topics | [A8](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a8-log-operations) | `ost, len, topic0, topic1` → `.` |
| 0xa3 | LOG3 | Append log record with three topics	| [A8](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a8-log-operations) | `ost, len, topic0, topic1, topic2` → `.` |
| 0xa4 | LOG4 | Append log record with four topics| [A8](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a8-log-operations) | `ost, len, topic0, topic1, topic2, topic3` → `.` |

### f0s: System operations
| Opcode | Name | Description | Gas  | Stack |
| :--- | :--- | :--- | :--- | :--- |
| 0xf0 | CREATE | Create a new account with associated code | [A9](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a9-create-operations) | `val, ost, len` → `addr` |
| 0xf1 | CALL | Message-call into an account | [AA](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#aa-call-operations) | `gas, addr, val, argOst, argLen, retOst, retLen` → `success` |
| 0xf2 | CALLCODE | Message-call into this account with alternative account's code | [AA](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#aa-call-operations) | `gas, addr, val, argOst, argLen, retOst, retLen` → `success` |
| 0xf3 | RETURN | Halt execution returning output data | 0* | `ost, len` → `.` |
| 0xf4 | DELEGATECALL | Message-call into this account with an alternative account's code, but persisting the current values for `sender` and `value` | [AA](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#aa-call-operations) | `gas, addr, argOst, argLen, retOst, retLen` → `success` |
| 0xf5 | CREATE2 | Create a child contract with a deterministic address | [A9](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#a9-create-operations) | `val, ost, len, salt` → `address` |

### Halt Execution, Revert, Mark for deletion
| Opcode | Name | Description | Gas  | Reference |
| :--- | :--- | :--- | :--- | :--- |
| 0xfd | REVERT | … | 0* | `ost, len` → `.` |
| 0xff | SELFDESTRUCT | Halt execution and register account for later deletion | 0 | `address` → `.` |

<br />

## References
- Ethereum [Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf)
- Ethereum's [Opcodes for the EVM](https://ethereum.org/en/developers/docs/evm/opcodes)
- EVM [Jello Paper](https://jellopaper.org/evm/)
- [Dynamic Gas Costs](https://github.com/wolflo/evm-opcodes/blob/main/gas.md#appendix---dynamic-gas-costs)
