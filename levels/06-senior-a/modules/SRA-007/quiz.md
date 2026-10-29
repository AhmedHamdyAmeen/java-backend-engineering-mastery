# SRA-007 · Large-scale performance — Quiz

Outcomes: O1 capacity forecasting · O2 workload modeling · O3 cost-performance optimization · O4 performance budgets.

**Q01 (O1)** Why plan capacity along the whole request path? A. The weakest link limits throughput B. Each service is independent C. It is cheaper D. Load tests are optional
**Q02 (O1)** The best basis for a three-year load forecast is: A. Last year's graph extended B. A guess C. Business drivers converted with measured ratios D. Competitor press releases
**Q03 (O1)** Showing low, base, and high cases is useful because: A. It is longer B. It reveals sensitivity to the growth assumption C. It avoids assumptions D. It replaces monitoring
**Q04 (O2)** A marketplace adds which new traffic shape? A. Only more browsing B. Static pages C. Bulk listing uploads and inventory sync D. Nothing new
**Q05 (O2)** Workload models are best validated by: A. Intuition B. Representative load tests and later comparison with production C. Waiting for an outage D. Vendor claims
**Q06 (O2)** For a new product with no history, the model should use: A. Nothing B. Zero C. Production data only D. Stated assumptions and analogies, later replaced by data
**Q07 (O3)** A common measure combining cost and performance is: A. Servers per team B. CPU percentage C. Cost per transaction at target latency D. Lines of code
**Q08 (O3)** Before accepting a saving that adds 10 ms latency, you should: A. Measure customer impact B. Deploy immediately C. Hide it D. Add more replicas
**Q09 (O4)** A performance budget gives each team: A. A bonus B. A limit on meetings C. A hardware allotment only D. A share of the end-to-end latency or cost target that it tracks
**Q10 (O4)** A team that exceeds its budget should: A. Be blamed B. Hide the metric C. Make a plan or renegotiate the budget with evidence D. Ignore it

## Answers
Q01 A · Q02 C · Q03 B · Q04 C · Q05 B · Q06 D · Q07 C · Q08 A · Q09 D · Q10 C

## Practical part
Six case exercises `SRA-007-EX01` to `EX06` plus the lab, reviewed as a capacity forecast. Pass: at least five of six exercises correct, quiz at least 8/10, and a forecast with explicit assumptions, growth sensitivity, and cost per order at target latency per year.
