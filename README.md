# clone-lin-balancer-bpt-in

Experimental **LIN** clone of Balancer V2 `WeightedMath._calcTokenInGivenExactBptOut`
(single-token join: tokens in for an exact BPT mint).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [balancer/balancer-v2-monorepo](https://github.com/balancer/balancer-v2-monorepo) `e91a2b643a49856f51a648d175667c1b48cf3377`
  - `WeightedMath.sol` sha256 `21c247fe3b45eb22511363aa1802f03766b476e8522dc33c1f29041ab9000cc8` blob `564887f01a497eb267e22aa22dae6799498ad859`
  - `FixedPoint.sol` sha256 `db8645a642a965744b15cbdedbf0214c6b8807cf98d359cfb00727a82967a944` blob `f3c74182db0cb5085ef3066ad069ecf76ef1df9f`
  - `LogExpMath.sol` sha256 `ed748287e341abc9b28972da8f075bbd2b00d1f1d28c6bbb16030e856b94b9fd` blob `3af242d4358d2da31fa485eeafd613df648f4e9a`
- **License of the algorithm:** GPL-3.0-or-later. This clone is original LIN/C11.
- **Class:** EXPERIMENTAL uint64-scale, `ONE = 1e9`. Not mainnet `ONE = 1e18` / LogExpMath / `uint256[]` joins.

## Files

- `src/lin_balancer_bpt_in.lin` — LIN kernel (`bbi_token_in(bal, w, bpt_out, supply, fee)`)
- `test/oracles/balancer_bpt_in_c11.c` — independent C11 `__int128` XOR limb oracle (not TCB)

## Reproduce proofs (in lin-open)

```bash
make balancer-bpt-in-proof
# or: python3 test/prove_balancer_bpt_in_external.py
```

Named goldens: 50/50 fee-0 on `1e9` balance/supply with `1e8` BPT out **210000000**
(`1.1^2-1`); 0.3% complement-weight fee **210315948**; 80/20 powUp 5/4
**126525059**. Naive linear `bal*bpt/supply` is **100000000** (2.1× undercharge).

## Not claimed

Uint256 / ONE=1e18 / LogExpMath mainnet parity. Multi-token array joins.
LIN replacing Balancer or the EVM. TVL or dollar savings. zk soundness.
`_calcBptOutGivenExactTokenIn` (see clone-lin-balancer-bpt-join).
