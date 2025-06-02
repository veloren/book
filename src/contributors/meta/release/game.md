# Release cycle

This page aims to document the release process of Veloren.
It first describes an overview and has more detailed chapters for single steps.

## Tasks

### 2 months before release

On the Sunday meeting:

1. Estimate a release date and communicate it to internal parties.
The date is subject to change until it becomes official later on.
2. Settle the following points:
   1. The theme of the release party.
   2. The features to implement with the release and those which would be nice-to-have.
   3. The people assigned to the party map.
      - The design of the party map.
   4. The people assigned to the release trailer.
      - The contents of the trailer.
   5. The people assigned to writing a blog post about the release.
   6. The people assigned to managing the feature freeze period.
   7. The people assigned to creating and publishing the release binaries.
   8. The people assigned to announcing the release on our social media accounts.
   9. The schedule for the release party:
      - The activities for the party.
      - The duration of each activity.
      - The people responsible for (each of) the activities.
3. Create a milestone on GitLab to track progress of the release.

### 1 month before release

On the Sunday meeting:

1. Choose an official release date when the core developers and the corresponding assignees are available.
2. Gather feedback about the activities and the trailer.
3. Discuss with the people responsible for the map:
    - What is the current state of the map?
    - What are their plans for the map?
    - Can they make the schedule?

| People in charge | Task |
|------------------|------|
| Feature freeze assignee(s) | Post the feature freeze schedule |
| Blog post assignee(s) | Write the blog post |
| Social media assignee(s) | Write the social media posts |
| Social media assignee(s) | Create an event on our Open Collective profile for the release party |

### 3 weeks before release

| People in charge | Task |
|------------------|------|
| Map assignee(s) | Prepare the map for the trailer |
| Activities assignee(s). | Prepare the activities for the trailer |
| Core developers | Review the map and the activities |
| Feature freeze assignee(s) | Gather feedback on what features are necessary, who will review them and when merge will be done |

### 2 weeks before release

| People in charge | Task |
|------------------|------|
| Trailer assignee(s) | Prepare the trailer for review |
| Core developers | Review the trailer |

### 1 week before release

| People in charge | Task |
|------------------|------|
| Feature freeze assignee(s) | Apply and watch the schedule over the next week |
| Map and activities assignee(s) | Wait until all tasks are completed |
| Trailer assignee(s) | Publish the trailer |
| Blog post assignee(s) | Publish the blog post |

### 8 hours before release

| People in charge | Task |
|------------------|------|
| Social media assignee(s) | Post the release announcement |
| Map and activities assignee(s) | Upload map and activities to the server |
| Release binaries assignee(s) | Merge the release commit and publish the release binaries |

### Sunday after release

On Sunday meeting:

- Discuss how the release party went.
  - What was done well?
  - What could have been done better?

## Plan for releasing the binaries

The sample commands in this section would be run for version 0.12.0 of the game.
Remember to adjust these commands to your applicable version.

1. Copy over `CHANGELOG.md`.
   - Update only the `server`, `client`, `server-cli` and `voxygen` crates.
   Other crates have an independent [semantic versioning](https://semver.org/).
   [Example MR](https://gitlab.com/veloren/veloren/-/merge_requests/3219)
2. Create a release branch from `master`:
    ```bash
    git checkout -b "r0.12"
    ```
3. Create a release tag:
    ```bash
    git tag -a "v0.12.0" -m "Version 0.12.0"
    ```
4. Push the release tag.
    ```bash
    git push --tag "v0.12.0"
    ```
5. Verify the release tag pipeline executed successfully.
    - <https://gitlab.com/veloren/veloren/-/pipelines>
6. Trigger a scheduled pipeline.
    - <https://gitlab.com/veloren/veloren/-/pipelines>
7. Verify the release container is built.
    - <https://gitlab.com/veloren/veloren/container_registry>
8. Add a link on the website to the release.
    - <https://veloren.net/download-other>
9. Create a release on GitLab.
10. Verify the release binaries have been copied to Wasabi.

## Social media cheat sheet

| Timeframe | Location | Notes |
|-----------|----------|-------|
| T-1 week | Discord | Ping the `@NewsPingSquad` and `@MediaPingSquad` roles. |
| T-30 mins | Discord | Ping the `@everyone` role. |
| T-8 hours | Reddit | The subreddit is `r/veloren`. |
| T-8 hours | Mastodon ||

## Templates

### GitLab milestone

```txt
# v0.xx Release

## People responsible
Blog post:
Trailer:
Map:
Feature freeze:
Release binaries:
Social media:

## Overview
Theme is: ``
Rough release day is: ``
Included features are:
-
Excluded features are:
-
Party schedule is:
- 18:00 UTC+00 start of party

## Checklist

Sunday meeting:
- [ ] Fixed release day is: `` *(T-1 month)*
- [ ] Map is approved by the core developers
- [ ] Activities are approved by core developers
- [ ] Trailer is approved by core developers

Blog:
- [ ] Release blog is prepared *(T-1 month)*
- [ ] Release blog is uploaded *(T-1 week)*

Trailer:
- [ ] Trailer is ready for review *(T-2 weeks)*
- [ ] Trailer is uploaded *(T-1 week)*

Map:
- [ ] Map is ready for review *(T-3 weeks)*
- [ ] Map is uploaded *(T-8 hours)*

Feature freeze:
- [ ] Freeze period is announced to public in #town-hall *(T-1 month)*
- [ ] Feature freeze is enforced *(T-1 week)*

Release binaries:
- [ ] Release binaries are produced, uploaded and verified *(T-8 hours)*

Social media:
- [ ] Posts are prepared *(T-1 month)*
- [ ] Posts are uploaded *(T-8 hours)*
```

### Feature freeze announcement

```txt
Hey @Contributor @DevPingSquad ,

**0.13 release is on Saturday, 2022-07-23 18:00 GMT**

As usual, there will be a **feature freeze** starting from 2022-07-16 18:00 GMT. We recommend submitting critical and large MRs for review now, before the feature freeze.

This release will also have a **stress test event** between the feature freeze and the release. We will be sharing further details of this later.

__Getting your large MR merged before feature freeze__
Please mention @xmac94x in the <#992383235332001942> thread with a short summary with the following details:

* What is complete.
* What needs to be done.
* Can your feature be partially introduced to master in its current state (as multiple MRs)?
* Do you foresee any issues with your MR and if so, which ones?
* Why should this feature be in 0.13?

This is required to align our testing and review strategies to ensure a smooth release.

**Schedule**
``
2022-07-16 18:00:00 GMT Feature freeze — No new feature MRs will be merged.
2022-07-18 18:00:00 GMT Stress test event.
2022-07-22 10:00:00 GMT Total freeze — no new merges will be introduced unless they're critical.
2022-07-22 16:00:00 GMT Release build will be compiled.
2022-07-23 12:00:00 GMT Main server hardware upgrade.
2022-07-23 18:00:00 GMT Release party!
``
```
