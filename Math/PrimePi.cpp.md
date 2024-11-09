---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links:
    - https://judge.yosupo.jp/problem/counting_primes
    - https://judge.yosupo.jp/submission/61551
    - https://www.facebook.com/code.cung.rr/posts/pfbid0eAyeQynkVN9evzy7Bnwx52zLeN7EHDE6H9Uur6KTSK2MTiyxJwCV71Wvujqz75vgl
    - https://www.spoj.com/problems/DIVCNT2/
    - https://www.spoj.com/problems/DIVFACT4/
    - https://www.spoj.com/problems/NTHPRIME/
    - https://www.spoj.com/status/SUMPRIM1,mr_invincible/
  bundledCode: "Traceback (most recent call last):\n  File \"/home/runner/.local/lib/python3.10/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir, options={'include_paths': [basedir]}).decode()\n  File \"/home/runner/.local/lib/python3.10/site-packages/onlinejudge_verify/languages/cplusplus.py\"\
    , line 187, in bundle\n    bundler.update(path)\n  File \"/home/runner/.local/lib/python3.10/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 401, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/home/runner/.local/lib/python3.10/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 260, in _resolve\n    raise BundleErrorAt(path, -1, \"no such header\"\
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: ../Prime/PrimePi.h:\
    \ line -1: no such header\n"
  code: "// prime_pi(n) = number of primes <= n\n//\n// Copied from https://judge.yosupo.jp/submission/61551\n\
    //\n// Tested:\n// - https://judge.yosupo.jp/problem/counting_primes\n// - https://www.spoj.com/problems/NTHPRIME/\
    \ (binary search + prime pi)\n//\n// Notes:\n// - There's simpler O(N^0.75) code\
    \ for prime_pi and prime_sum\n//   Write up: https://www.facebook.com/code.cung.rr/posts/pfbid0eAyeQynkVN9evzy7Bnwx52zLeN7EHDE6H9Uur6KTSK2MTiyxJwCV71Wvujqz75vgl\n\
    //   Implementation:\n//   - prime_sum: https://www.spoj.com/status/SUMPRIM1,mr_invincible/\n\
    //   - prime_pi: https://www.spoj.com/problems/DIVCNT2/\n//   This can be modified\
    \ to implement more complicated things such as\n//   https://www.spoj.com/problems/DIVFACT4/\n\
    \n// prime_pi {{{\nusing ll = long long;\nint isqrt(ll n) {\n    return sqrtl(n);\n\
    }\nll prime_pi(const ll N) {\n    if (N <= 1) return 0;\n    if (N == 2) return\
    \ 1;\n    const int v = isqrt(N);\n    int s = (v + 1) / 2;\n    vector<int> smalls(s);\n\
    \    for (int i = 1; i < s; i++) smalls[i] = i;\n    vector<int> roughs(s);\n\
    \    for (int i = 0; i < s; i++) roughs[i] = 2 * i + 1;\n    vector<ll> larges(s);\n\
    \    for (int i = 0; i < s; i++) larges[i] = (N / (2 * i + 1) - 1) / 2;\n    vector<bool>\
    \ skip(v + 1);\n    const auto divide = [](ll n, ll d) -> int { return (double)n\
    \ / d;};\n    const auto half = [](int n) -> int { return (n - 1) >> 1;};\n  \
    \  int pc = 0;\n    for (int p = 3; p <= v; p += 2) if (!skip[p]) {\n        int\
    \ q = p * p;\n        if ((ll)q * q > N) break;\n        skip[p] = true;\n   \
    \     for (int i = q; i <= v; i += 2 * p) skip[i] = true;\n        int ns = 0;\n\
    \        for (int k = 0; k < s; k++) {\n            int i = roughs[k];\n     \
    \       if (skip[i]) continue;\n            ll d = (ll)i * p;\n            larges[ns]\
    \ = larges[k] - (d <= v ? larges[smalls[d >> 1] - pc] : smalls[half(divide(N,\
    \ d))]) + pc;\n            roughs[ns++] = i;\n        }\n        s = ns;\n   \
    \     for (int i = half(v), j = ((v / p) - 1) | 1; j >= p; j -= 2) {\n       \
    \     int c = smalls[j >> 1] - pc;\n            for (int e = (j * p) >> 1; i >=\
    \ e; i--) smalls[i] -= c;\n        }\n        pc++;\n    }\n    larges[0] += (ll)(s\
    \ + 2 * (pc - 1)) * (s - 1) / 2;\n    for (int k = 1; k < s; k++) larges[0] -=\
    \ larges[k];\n    for (int l = 1; l < s; l++) {\n        ll q = roughs[l];\n \
    \       ll M = N / q;\n        int e = smalls[half(M / q)] - pc;\n        if (e\
    \ < l + 1) break;\n        ll t = 0;\n        for (int k = l + 1; k <= e; k++)\n\
    \            t += smalls[half(divide(M, roughs[k]))];\n        larges[0] += t\
    \ - (ll)(e - l) * (pc + l - 1);\n    }\n    return larges[0] + 1;\n}\n// }}}\n\
    //Example Code\n#define PROBLEM \"https://judge.yosupo.jp/problem/counting_primes\"\
    \n\n#include <bits/stdc++.h>\nusing namespace std;\n\n#include \"../Prime/PrimePi.h\"\
    \n\nint32_t main() {\n    ios::sync_with_stdio(0); cin.tie(0);\n    long long\
    \ n; cin >> n;\n    cout << prime_pi(n) << endl;\n    return 0;\n}"
  dependsOn: []
  isVerificationFile: false
  path: Math/PrimePi.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: Math/PrimePi.cpp
layout: document
redirect_from:
- /library/Math/PrimePi.cpp
- /library/Math/PrimePi.cpp.html
title: Math/PrimePi.cpp
---