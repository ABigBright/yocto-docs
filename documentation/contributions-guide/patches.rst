.. SPDX-License-Identifier: CC-BY-SA-2.0-UK

*******
Patches
*******

It is inevitable that software being built by the project will need
to be patched at some point. These patches can be extremely useful
and improve functionality, add features, fix bugs or many other things.
They can also become a maintenance burden if the wrong approach is taken.

There are some best practises when dealing with patches. At the time of 
writing a patch you likely know a lot about the circumstances but it is
important to record it so that it can be recalled at a later date and also
understood by others. Ideally a patch should:

Document what the patch does
  Sometimes it can be obvious from reading the patch what it does but
  even then, a summary of what a change is doing is useful.

Document *why* the patch is needed
  As well as saying what the patch does, it is important to say *why* it
  is doing it. If it solves a bug, explain what that bug is. Summarise what 
  the issue the patch solves is and make the case for why we need the change.

Link to any discussions, bug trackers or other useful information
  Including a link to any discussions of the change with upstream, or any
  related discussion in a bug tracker or mailing list can be helpful for
  anyone wanting to find out more about the patch. These should be seen
  as a way to help someone find out more, not to replace descriptions in
  the patch. It may also be helpful to link to any commits related to the 
  patch.

Summarise the status of the patch with it's upstream
  If the patch is useful or solves a problem, the chances are that the upstream
  software you're patching may be interested in the change. Documenting whether
  a discussion has happened with that upstream is helpful so maintainers can
  make decisions about the patch as that upstream software changes.

Document who wrote the patch and license information
  Documenting who wrote the patch, when and that license information has 
  been handled is helpful and means people know who to discuss the patch with.
  This information can often be summarised by adding your Signed-off-by: line 
  which as well as your details, also records the license situation for projects 
  which use that convention but is generally useful. The date, whilst not essential, 
  does give a quick idea of how old the patch is.

It can be really helpful to write all this information into the patch as if
you were writing a change you were about to send to upstream. That usually
means a shortlog/one-line summary, a more detailed description, links to any
linked bug tracking report and the author's name/email address. The only addition
besides this would be an Upstream-Status line which is for our tracking purposes
and wouldn't be included in any upstream submission.


Patch Upstream-Status
=====================

The Yocto Project has adopted the convention of using an *Upstream-Status:* line
in patches to summarise it's status, for example::

    Upstream-Status: Inappropriate [OpenEmbedded specific configuration]
    
could be used to denote a patch which was adding configuration specific to 
OpenEmbedded usage which would not be appropriate to send upstream.

We support the following status 'states':

Pending
  No determination has been made yet or not yet submitted to upstream

Submitted [where]
  Submitted to upstream, waiting approval
  Optionally include where it was submitted, such as the author's email 
  address, mailing list, etc.

Backport [link to commit]
  The patch was accepted upstream and applied to the software
  The patch will now be a backport from the upstream source control system


Denied [reason]
  Not accepted by upstream, include reason in patch

Inactive-Upstream [lastcommit: when (and/or) lastrelease: when]
  The upstream is no longer available. This typically means a defunct project 
  where no activity has happened for a long time - measured in years. To make
  that judgement, it is recommended to look at not only when the last release 
  happened, but also when the last commit happened, and whether newly made bug 
  reports and merge requests since that time receive no reaction. It is also
  recommended to add any relevant links to the commit message where the inactivity
  can be clearly seen.

Inappropriate [reason]
  The patch is not appropriate for upstream, include a brief reason

CVE Patches
===========

In order to allow auditing of vulnerabilities, patches that fix CVEs must should contain a *CVE:* tag. This tag list all CVEs fixed by the patch. If more than one CVE is fixed, separate them using spaces.


An example of a patch that fixes grub2 CVE-2015-8370::

  grub2: Fix CVE-2015-8370
  
  [No upstream tracking] -- https://bugzilla.redhat.com/show_bug.cgi?id=1286966
  
  Back to 28; Grub2 Authentication
  
  Two functions suffer from integer underflow fault; the grub_username_get() and grub_password_get()located in
  grub-core/normal/auth.c and lib/crypto.c respectively. This can be exploited to obtain a Grub rescue shell.
  
  Upstream-Status: Accepted [http://git.savannah.gnu.org/cgit/grub.git/commit/?id=451d80e52d851432e109771bb8febafca7a5f1f2]
  CVE: CVE-2015-8370
  Signed-off-by: Joe Developer <joe.developer@example.com>


