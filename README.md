## CNV Release Note Process

### Jira Tickets

You will be assigned four Jiras. Below are the Jiras and in the suggested order to work them:

1. Create a "shell" file for the release notes
2. Create a "placeholder" file for the release notes
3. Review the known issues and bug fixes
4. Update and assemble the CNV release notes

#### Release Note Shell File

A "shell" file will need to be created so that writers can start adding release notes. The process is essentially copying over the previous version's release note file and preparing it for the new version by:

* Updating the release notes file name and anchor IDs
* Removing all content under *New and changed features* but making sure to leave headers
* Removing *Bug fixes* content
* Removing *Removed features* content

This is a step by step process with commands included. Be sure to replace `4.16` and `4.17` with the versions you are working with.

1. Check out the branch of the new version:
   * `$ git checkout enterprise-4.17 ; git fetch upstream`
2. Create a feature branch off of the enteprise branch:
   * `$ git checkout -b CNV-XXXX`
3. Rename the old version filename to the new version filename:
   * `$ git mv virt/release_notes/virt-4-16-release-notes.adoc virt/release_notes/virt-4-17-release-notes.adoc`
4. Replace all old version strings with the new version strings in the release notes file:
   * `$ sed -i 's/virt-4-16/virt-4-17/g' virt/release_notes/virt-4-17-release-notes.adoc`
5. Replace old version string with the new version string in the `_topic_map.yml` file:
   * `$ sed -i 's/virt-4-16-release-notes/virt-4-17-release-notes/g' _topic_maps/_topic_map.yml`
6. Remove all content under *New and changed features*, *Bug fixes*, and *Removed features* in the release-note file while making sure to leave the headers of the sections.
7. Save all changes and submit your pull request.

**Example PR**: [Link](https://github.com/openshift/openshift-docs/pull/79779)

### Release Note Placeholder File

For builds and tests to be successful in your GitHub pull request, you must open a separate PR to add a dummy release notes file to the main branch. This is a step by step process with commands included. Be sure to replace `4.17` with the version you are working on.

1. Check out the branch of the new version:
   * `$ git checkout main ; git fetch upstream`
2. Create a feature branch off of the main branch:
   * `$ git checkout -b CNV-XXXX`
3. Create a new placeholder file with the new version name:
   * `$ touch virt/release_notes/virt-4-17-release-notes.adoc`
4. Place the contents below into that file and save it.
    ```
    :_content-type: ASSEMBLY
    [id="virt-4-17-release-notes"]
    = {VirtProductName} release notes
    include::_attributes/common-attributes.adoc[]
    :context: virt-4-17-release-notes
    toc::[]
    
    Do not add or edit release notes here. Edit release notes directly in the branch
    that they are relevant for.
    
    This file is here to allow builds to work.
    ```
5. Save all changes and submit your pull request.

**Example PR**: [Link](https://github.com/openshift/openshift-docs/pull/79783)
