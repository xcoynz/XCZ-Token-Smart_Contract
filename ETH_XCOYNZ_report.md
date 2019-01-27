# XCOYNZ token security audit report

# Summary

This is the report from a security audit performed on [xcoynz](https://github.com/xcoynz/XCZ-Token-Smart_Contract/blob/master/XCOYNZ%20Test%20SC.sol) by [gorbunovperm](https://github.com/gorbunovperm).

> Smart Contract to support XCOYNZ token and project fundamentals with 1.25B total supply and a token ticker of XCZ. 
The Smart Contract encompasses all basic token attributes and periodic releases of tokens, adhering to vesting periods as dictated by the project's long term vision which is made publicly available in the Whitepaper and all project documentation.

https://xcoynz.com/

# In scope

Commit hash: `e4535fb03b4621919fba7798a0721111f35f634b`

1. [XCOYNZ Test SC.sol](https://github.com/xcoynz/XCZ-Token-Smart_Contract/blob/e4535fb03b4621919fba7798a0721111f35f634b/XCOYNZ%20Test%20SC.sol)


# Findings

In total, **2 issues** were reported including:

- 0 high severity issue.

- 1 medium severity issues.

- 1 low severity issues.

- 0 minor observations.

## Security issues

### 1. Known vulnerabilities of ERC-20 token

#### Severity: low

#### Description

* It is possible to double withdrawal attack. More details [here](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit)

* Lack of transaction handling mechanism issue. [WARNING!](https://gist.github.com/Dexaran/ddb3e89fe64bf2e06ed15fbd5679bd20) This is a very common issue and it already caused millions of dollars losses for lots of token users! More details [here](https://docs.google.com/document/d/1Feh5sP6oQL1-1NHi-X1dbgT3ch2WdhbXRevDN681Jv4/edit)

### Recommendation

Add into a function `transfer(address _to, ... )` following code:
```solidity
require( _to != address(this) );
```

### 2. It is possible to bypass the restrictions for the owner

#### Severity: medium

#### Code snippet

* [XCOYNZ Test SC.sol](https://github.com/xcoynz/XCZ-Token-Smart_Contract/blob/e4535fb03b4621919fba7798a0721111f35f634b/XCOYNZ%20Test%20SC.sol#L367-L375)

#### Description

There is the restrictions for the tokens owner in `transfer` function. But there is no restrictions for `transferFrom` function and the `tokenOwner` can using an intermediary address to bypass the restrictions.


# Conclusion

There is some serious vulnerabilities were found here.