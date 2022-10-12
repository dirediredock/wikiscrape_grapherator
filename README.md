# wikigraph_infovis

This project is about a data-driven infographic of programming languages, a network graph visualization of how languages influence each other and develop over time. Project for 2022 CPSC547 (Information Visualization) at UBC.

The data comes from Wikipedia, specifically from English pages (.en) that have an "infobox" HTML tag, which has href links that can be recursively Python scraped to construct a network graph adjacency matrix. In this graph each unqiue PL is a node, and relationships between nodes is determined by how PLs influence one another. Supplementary data includes year of first appereance, and can be expanded to include programming paradigm and typing discipline, for example.

### Git Setup Cheatsheet

First download the repo through CLI and use `checkout -b` to create and name a new branch.

```
cd src
gh repo clone dirediredock/wikigraph_infovis
cd wikigraph_infovis
git status
git checkout -b desktop_edits
git status
```

When work of the day is complete, commit all changes on VS Code and `push`, then return to `main` for a fresh start next time.

```
git push
git push --set-upstream origin desktop_edits
git fetch origin main:main
git checkout main
```

## Data Exploration

<img src="figures/wikiscrape_results_2.png" width="100%">

- Data cleaning: removing `href` vestigial disambiguator string and duplicates, export node-to-node directed graph as CSV (each row is a unique graph edge)
- Metadata: isolate in dictionaries, then dataframe, then export as CSV

<img src="figures/summary_A_plot.png" width="50%"><img src="figures/summary_A_text.png" width="50%">
<img src="figures/summary_B_plot.png" width="50%"><img src="figures/summary_B_text.png" width="50%">
<img src="figures/adjacency_forwards.png" width="50%"><img src="figures/wikigraph_shell_layout.png" width="50%">
<img src="figures/pyvis_1.png" width="50%"><img src="figures/pyvis_2.png" width="50%">

Forced directed network drawn with `pyvis.network` with `force_atlas_2based()`, on the right with MATLAB node and neighbors highlighted.

# Notes

- Tasky explainer, guided by "here is something that I'd like to know!"
- Try to think about tasks (highlight path, two-way influence nodes, year-sorted)
- Domain specific first, then abstract
- For this abstraction, there can be generalized - a more technique-y paper
- - node with mayor influence
- trace/centrality

What to do with nodes with missing year?

- We know the year must be larger than the smallest year of an incoming node
- We can calculate the average difference of node and subnode year difference to calculate a buffer year addition so that

- `unknown_year = min([list_incoming_node_years]) + year_buffer`

Maybe I can make the length of the edge realted to time?

- `edge_length = end_node_year - start_node_year`

Topology tasks

- Pick a node, highlight all paths incoming and outgoing from it
- Pick a node, highlight all the nodes just one hop away
- Shortest path between two nodes
- Are there bridge nodes between network clusters?
