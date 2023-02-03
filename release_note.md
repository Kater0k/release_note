# Changelog: 
## Feature
### Catalog
PR: [ add no_fs report status for data_items ](https://github.com/elastio/blue-stack/pull/5958)
- As we discussed on daily, there is a case when fs-check does not contain partitions, it supposed to mean that there is empty no_fs volume. So here:
1) When show data_item_snapshots we now for such volumes return no_fs status
2) We now do not show in list or filter values reports that have no partitions at all, or separate volumes with no partitions.

- Ticket(s): Not specified
- Author(s): rkaiafiuk@elastio.com
- Commit hash: [5e19d8bfeb19cbe15fe113bf7c9b3091c3b0ad9c](https://github.com/elastio/blue-stack/commit/5e19d8bfeb19cbe15fe113bf7c9b3091c3b0ad9c)
- QA tips:
  - Not specified
***
### E2e
PR: [ #5301 - add cc installation using ui to e2e tests ](https://github.com/elastio/blue-stack/pull/5925)
- Added scenario with Cloud Connector installation using UI to e2e tests
- Ticket(s): [5301](https://github.com/elastio/blue-stack/issues/5301)
- Author(s): skiptomy55@gmail.com
- Commit hash: [d60bc9f583615d403f9a5643a230b542432752e6](https://github.com/elastio/blue-stack/commit/d60bc9f583615d403f9a5643a230b542432752e6)
- QA tips:
  - Not specified
***
### Infra
PR: [ promtail: add cri parsing pipeline ](https://github.com/elastio/blue-stack/pull/5954)
- It looks like with 1.24 k8s new logging format has been introduced, k8s-logs, thus promtail parsing had to be adjusted to ease Grafana logs manipulation on users' side.
- Ticket(s): [5951](https://github.com/elastio/blue-stack/issues/5951)
- Author(s): 75213+ivankovnatsky@users.noreply.github.com
- Commit hash: [a53ef365728a84fff23247a81f2cb684c8143630](https://github.com/elastio/blue-stack/commit/a53ef365728a84fff23247a81f2cb684c8143630)
- QA tips:
  - Not specified
***
### Reports
PR: [ #5590 - rename reports columns for csv export ](https://github.com/elastio/blue-stack/pull/5962)
- Report templates cells were remained in accordance with data fields names for csv export; 
- Empty Backup Date value is set to empty string
- Ticket(s): [5590](https://github.com/elastio/blue-stack/issues/5590)
- Author(s): lagutochkina@gmail.com
- Commit hash: [6cf55ef4b37a2e54dec4412350da2b1744bc0f9a](https://github.com/elastio/blue-stack/commit/6cf55ef4b37a2e54dec4412350da2b1744bc0f9a)
- QA tips:
  - Not specified
***
PR: [ #5590 - update dashboard and reports templates ](https://github.com/elastio/blue-stack/pull/5947)
- Dashboard and reports templates were updated:
- "Account Alias" column was added
- Columns names were updated
- Statuses names were mapped to the new names
- Countable field "TimeToCompleteBackup" was added with appropriate formula
- "BackupDaysOld" is now a countable from "MinutesSince" (days from minutes formula)
- All "N/A" values were replaced with required values (empty string or 0)
- Ticket(s): Not specified
- Author(s): lagutochkina@gmail.com
- Commit hash: [8f2b88212cd6314a4d7bc40ebad66e94f39f8fcb](https://github.com/elastio/blue-stack/commit/8f2b88212cd6314a4d7bc40ebad66e94f39f8fcb)
- QA tips:
  - Not specified
***
## Fix
### Infra
PR: [ vmagent: add pdb and increase replica count ](https://github.com/elastio/blue-stack/pull/5924)
- We need to make sure that we service at least half of the victoria
metrics workload during disruptions and deployments.
- Ticket(s): Not specified
- Author(s): 75213+ivankovnatsky@users.noreply.github.com
- Commit hash: [d990cacf98544263d2aed0333fb119ba8be0b4ee](https://github.com/elastio/blue-stack/commit/d990cacf98544263d2aed0333fb119ba8be0b4ee)
- QA tips:
  - Not specified
***
### Pechkin
PR: [ fix elastio:backup-policy:compliance-check:succeeded having wrong end time label ](https://github.com/elastio/blue-stack/pull/5964)
- There was a type in label value causing the same timestamp to be used for both start and end.
- Ticket(s): Not specified
- Author(s): abarkovsky@elastio.com, anton@swarmer.me
- Commit hash: [b14bcc08615b8ac4975bdc5edd2dc54c926416bb](https://github.com/elastio/blue-stack/commit/b14bcc08615b8ac4975bdc5edd2dc54c926416bb)
- QA tips:
  - Not specified
***
## Revert
### Infra
PR: [ enable istio in monitoring namespace ](https://github.com/elastio/blue-stack/pull/5955)
- We needed it to be disabled to make Victoria Metrics migration work.
- Ticket(s): Not specified
- Author(s): 75213+ivankovnatsky@users.noreply.github.com
- Commit hash: [30d3b511b79b3f68bebf3a64774a85fe2ed17d57](https://github.com/elastio/blue-stack/commit/30d3b511b79b3f68bebf3a64774a85fe2ed17d57)
- QA tips:
  - Not specified
***
 # Post-release tasks: 
## Pechkin
PR: [ fix elastio:backup-policy:compliance-check:succeeded having wrong end time label ](https://github.com/elastio/blue-stack/pull/5964)
- Ticket(s): Not specified
- Author(s): abarkovsky@elastio.com, anton@swarmer.me
- Commit hash: [b14bcc08615b8ac4975bdc5edd2dc54c926416bb](https://github.com/elastio/blue-stack/commit/b14bcc08615b8ac4975bdc5edd2dc54c926416bb)
- Once the release has been fully deployed:
Delete all events of kind `elastio:backup-policy:compliance-check:succeeded`.
Then run the following command for the pechkin service:
```bash
./app --config configs/config.yaml regenerate-backup-window-succeeded-events
```
This command will regenerate all `elastio:backup-policy:compliance-check:succeeded` events and throw them into the `notifications` service.
***
