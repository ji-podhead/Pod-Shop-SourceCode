## 2. The Pod Shop
<div align="center">
 <div style="display: flex; justify-content: space-between; width: 100%;">
   <!-- Stellen Sie sicher, dass der Container genügend Platz hat -->
   <div style="width: 50%; display: flex; justify-content: center; box-sizing: border-box;">
	 <a href="https://github.com/ji-podhead/Pod-Shop-SourceCode">  
    <b>SourceCode Repo</b>
    </a>
   </div>
   <div style="width: 50%; display: flex; justify-content: center; box-sizing: border-box;">
    <a href="https://github.com/ji-podhead/Pod-Shop-App-Configs/blob/main/README.md">  
    <b>App Config Repo</b>
    </a>
   </div>
 </div>
</div>






![POD SHOP](https://github.com/ji-podhead/DevOps/blob/main/pod-shop-infrastructure.png?raw=true)

---

### Release Management & Test Scheduling
***successfull Production-Commits will be pushed to `release-candidate` Branch***

| Phase | Description | Branch | Frequency | Crontab Time |
|---|---|---|---|---|
| Development | Commits trigger Jenkins CI-CD pipeline | production | On demand | * * * * * |
| IAC | Scanns the App Configuration folder | test |Snyk IAC (5 per day max) and Checkov on demand |  * * * * * |
| Compliance | Compliance Checks, IAM Policy Validation, Network Policy Enforcement, Topology Verification | test | Every 4 hours | 0 */4 * * * |
| WebSecurity | Running Web and Application Security Tests to avoid hacks like xss | test | Every 4 hours | 0 */4 * * * |
| Integration | Executing Integration Tests (Back & Frontend) | test | 16:00 and 22:00 daily | 0 16,22 * * * |
| Performance | Cluster-wide back- and frontend performance test  | test | 16:30 and 22:30 daily | 30 16,22 * * * |
| Build | Building the final version of the application for release | release-candidate | 23:00 daily | 0 23 * * * |
| Release | Deploying the built application to production | production & release | 24:00 daily | 0 0 * * * |


---
