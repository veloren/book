# Release Cycle

This page aims to document the release process of veloren. It first describes an overview and has more detailed chapters for single steps

## Tasks

### When: 2 month before release
#### Where: Sunday Meeting
- roughly select a release-date and communicate that to internal parties (Note: it might be changed is not official yet!)
- The following questions are answered:
    - What is the theme of this party
    - what features should be definitely in it, what features might get in
    - a map responsible is chosen, we plan how it will look like
    - a trailer responsible is chosen, we plan what it should contain
    - a release blog writer is chosen
    - a responsible for the feature freeze is chosen
    - a responsible for the release-binary is chosen
    - a responsible for social-media posts is chosen
    - a schedule for the party is created, we plan activities, how long they will take and responsibles for those activities
- a gitlab Milestone is created to track progress of this release.

### When: 1 month before release
#### Where: Sunday Meeting
- pick a final release date when core devs (e.g. Angle, xMac) are available and responsibles can make it.
- feedback from the activities, trailer and map responsibles is discussed, what is their state, what do they plan. Do they need to adjust? Can they make the schedule?

#### Who: feature freeze-responsible
- feature freeze schedule is posted

#### Who: Blog post responsible
- Blog is prepared and written

#### Who: Social Media responsible
- Posts are prepared and written

### When: 3 weeks before release
#### Who: Map responsible
- Map is ready enough for the trailer

#### Who: Activities responsible
- Activities are ready enough for the trailer

#### Who: Core Devs
- Map and Activities are reviewed by Core Devs

#### Who: Feature Freeze responsible
- Features that are necessary are collected and are planned who reviews and merging is done.

### When: 2 weeks before release
#### Who: trailer responsible
- Trailer is ready enough to be reviewed

#### Who: Core Devs
- Trailer is reviewed by Core Devs

### When: 1 week before release
#### Who: Feature Freeze responsible
- Schedule is applied over the next week and watched by responsible

#### Who: map/activities
- all tasks are completed and are waiting to be executed

#### Who: trailer responsible
- the trailer is uploaded and live

#### Who: Blog post responsible
- the Blog post is uploaded and live

### When: 8 hours before release
#### Who: Social Media Responsible
- Posts are done

#### Who: map/activities
- upload map and activities to the server

#### Who: release-binary responsible
- Release commit is merged and Release Binaries are distributed

### When: Sunday after release
#### Where: Sunday Meeting
- Discuss pro and contra of the release party

## Details:
### Gitlab Milestone
```
# v0.xx Release

## Responsibles
blog:
trailer:
map:
feature-freeze:
release-binary:
social-media:

## Overview
Theme is: ``
Rough Release day is: ``
Included features are:
-
Excluded features are:
-
Party Schedule is:
- 18:00 GMT+0 start of party

## Checklist

Sunday Meeting:
- [ ] Fixed Release day is: `` *(T-1 month)*
- [ } Map is approved by CoreDevs
- [ } Activities are approved by CoreDevs
- [ } Trailer is approved by CoreDevs

Blog:
- [ ] release blog is prepared *(T-1 month)*
- [ ] release blog is uploaded *(T-1 week)*

Trailer:
- [ ] trailer is ready for review *(T-2 weeks)*
- [ ] trailer is uploaded *(T-1 week)*

Map:
- [ ] map is ready for review *(T-3 weeks)*
- [ ] map is uploaded *(T-8 hours)*

Feature-freeze:
- [ ] freeze-period is announced to public in #town-hall *(T-1 month)*
- [ ] Feature Freeze is enforced *(T-1 week)*

Release-Binary:
- [ ] Release Binaries are producuded uploaded and verified *(T-8 hours)*

Social-Media:
- [ ] posts are prepared *(T-1 month)*
- [ ] posts are uploaded uploaded *(T-8 hours)*
```

### Social-Media plan
- T-1 week    @NewsPingSquad @MediaPingSquad
- T-30 mins   @everyone
- T-8 hours   reddit/<insertsubreddithere>
- T-8 hours   twitter

### Feature Freeze Posts

```
Hey @Contributor  @DevPingSquad ,

**0.13 release is on Saturday, 2022-07-23 18:00 GMT**

As usual, there will be a **feature freeze** starting from 2022-07-16 18:00 GMT. We recommend submitting critical and large MRs for review now, before the feature freeze.

This release will also have a **stress test event** between the feature freeze and the release. We will be sharing further details of this later.

__Getting your large MR merged before feature freeze__
Please mention @xMAC94x#2493  in the <#992383235332001942> thread with a short summary with the following details (the more, the better):
* What is complete
* What needs to be done
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

### Binary Release Plan

1. Copy over CHANGELOG, update only `server`, `client`, `server-cli`, `voxygen` crates - the others are on a independent [semver](https://semver.org/).
[example MR](https://gitlab.com/veloren/veloren/-/merge_requests/3219)
2. create release branch from master `git checkout -b "r0.12"`
3. create release tag `git tag -a "v0.12.0" -m "release 0.12.0"`
4. push release tag `git push --tag "v0.12.0"`
5. verify a release tag pipeline runs: https://gitlab.com/veloren/veloren/-/pipelines
6. verify release container is build: https://gitlab.com/veloren/veloren/container_registry
7. add link to https://veloren.net/download-other/
8. create a release on gitlab
9. verify a release binary is copied to wasabi