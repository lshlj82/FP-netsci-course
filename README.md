# The Friendship Paradox: An Interactive Demo

An in-browser demo of the friendship paradox: why your friends have more friends than you do on average, why there are two different averages behind that statement, and why neither one tells you whether *most* people's friends have more friends.

Created by Claude Opus 5.5, based on the lecture slides and papers by Sang Hoon Lee.

## What's inside

The page is a single self-contained `index.html`. It has no build step. Its only outside resources are two Google Fonts (Source Serif 4 and IBM Plex Sans) and KaTeX 0.16.9 from cdnjs, which typesets the formulas. Without them the page falls back to system fonts and shows the formulas as plain TeX. All networks are generated and measured live in the browser, and the karate club and college football networks are embedded in the file. It shares its look and chart code with the companion scale-free networks and network centrality demos.

The demo has five parts:

1. **Ask everyone.** The four-person star from the slides and the seven-friend network from Menczer, Fortunato and Davis. Every person is labeled with k and k_nn, and the three averages are written out term by term in the style of the slides: (1 + 1 + 1 + 3)/4 = 1.5, (3 + 3 + 3 + 1 + 1 + 1)/6 = 2, and (3 + 3 + 3 + 1)/4 = 2.5. For the seven-friend network the last one is 17/6, as in the textbook. Picking a person highlights their friends.
2. **It is a sampling bias.** Three samplers survey a network: a random person, the end of a random friendship, and a random friend of a random person. The sampled degree distributions converge to p(k) and q(k) = kp(k)/⟨k⟩, and the running averages converge to ⟨k⟩, ⟨k_friend⟩ = ⟨k²⟩/⟨k⟩ and ⟨k_nn⟩. Networks: scale-free and random with 10,000 nodes, Zachary's karate club, and college football.
3. **Two ways to average your friends' friends.** The x + 1/x ≥ 2 proof of the ego-based version, then Feld's Fig. 4: four arrangements of the same degrees with ⟨k_friend⟩ = 2 throughout and ⟨k_nn⟩ = 1.5, 2.0, 2.17 and 2.5, along with Feld's 60%, 67% and 75%. A rewiring experiment applies degree-preserving swaps to a 1,000-node scale-free network and checks three expressions for ⟨k_friend⟩ − ⟨k_nn⟩ against each other on every step: the direct difference, Cov_n(k, k_nn)/⟨k⟩, and the inversity formula of Kumar, Krackhardt and Feld. A complete bipartite network K_{m,n} with adjustable m and n confirms ⟨k_nn⟩ = (m² + n²)/(m + n) = ⟨k³⟩/⟨k²⟩ and r = −1.
4. **Do most people's friends have more friends?** φ_global (the share of nodes with k_i < k_nn(i)) and φ_local (the share with hub centrality h_i < 1/2) for the five-node toy network, the karate club, college football, and generated networks. Each node is colored by which kind of domination applies, and a quadrant plot of h_i against k_i − k_nn(i) follows panel (c) of Figs. 2 and 3 in the JKPS paper. The values reproduce Table 1 of that paper exactly.
5. **The generalized friendship paradox.** Each node gets a log-normal attribute whose correlation with log degree you set. The page shows the share of people whose friends' mean exceeds their own and the share for whom most friends have more. It also shows why the mean-based share is above one half even with no link to degree.

## Running it

Open `index.html` in any modern browser. To host it with GitHub Pages, push this folder as a repository and enable Pages for the branch that contains `index.html`.

## Models and methods

- **Averages.** ⟨k_friend⟩ = Σ k_i² / Σ k_i (alter-based) and ⟨k_nn⟩ = N⁻¹ Σ_i k_nn(i) with k_nn(i) = k_i⁻¹ Σ_j a_ij k_j (ego-based). The identity ⟨k_friend⟩ − ⟨k_nn⟩ = Cov_n(k, k_nn)/⟨k⟩ follows from ⟨k k_nn⟩ = ⟨k²⟩.
- **Inversity.** ρ is the Pearson correlation over oriented edges between the destination degree and the inverse origin degree. The page checks ⟨k_nn⟩ − ⟨k_friend⟩ = ρ √[(κ₁κ₃ − κ₂²)(κ₋₁ − κ₁⁻¹)/κ₁], with κ_m = ⟨k^m⟩.
- **Majority fractions.** h_i counts neighbors with strictly smaller degree, so ties count as neither higher nor lower, as in the paper.
- **Assortativity** r is Newman's edge-based Pearson coefficient.
- **Generated networks** use Barabási–Albert preferential attachment with m = 2 and Erdős–Rényi G(N, M) with ⟨k⟩ = 4, keeping the largest connected component.
- **Rewiring** uses double-edge swaps that never change a degree or create self-loops or multi-edges. Toward assortative, the two highest-degree endpoints are joined; toward disassortative, the highest is joined with the lowest.
- **Attributes** in the generalized section are x_i = exp(ρ z_i + √(1 − ρ²) ε_i), where z_i is the standardized log degree and ε_i is standard normal noise.
- **Data.** The karate club is NetworkX's `karate_club_graph()`. College football is M. E. J. Newman's `football.gml` (Girvan and Newman, 2002), with team names and conferences.

## References

- S. L. Feld, "Why your friends have more friends than you do," *Am. J. Sociol.* 96, 1464 (1991).
- V. Kumar, D. Krackhardt, and S. Feld, "On the friendship paradox and inversity," *Proc. Natl. Acad. Sci. USA* 121, e2306412121 (2024).
- S. H. Lee, "Two variants of the friendship paradox: The condition for inequality between them," *New Phys.: Sae Mulli* 76, 169 (2026).
- S. H. Lee, "Friendship-paradox paradox: do most people's friends really have more friends than they do?," *J. Korean Phys. Soc.* 88, 890 (2026).
- M. E. J. Newman, "Assortative mixing in networks," *Phys. Rev. Lett.* 89, 208701 (2002).
- M. E. J. Newman, "Ego-centered networks and the ripple effect," *Social Networks* 25, 83 (2003).
- Y.-H. Eom and H.-H. Jo, "Generalized friendship paradox in complex networks: The case of scientific collaboration," *Sci. Rep.* 4, 4603 (2014).
- F. Menczer, S. Fortunato, and C. A. Davis, *A First Course in Network Science* (Cambridge University Press, 2020), Chapter 3.
- W. W. Zachary, *J. Anthropol. Res.* 33, 452 (1977); M. Girvan and M. E. J. Newman, *Proc. Natl. Acad. Sci. USA* 99, 7821 (2002).

See also the companion explorer at https://lshlj82.github.io/friendship-paradox/.
