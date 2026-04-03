---
layout: home
title: 🏠 Home
nav_exclude: false
nav_order: 1
---

# {{ site.tagline }}

{: .mb-2 }
{{ site.description }}
{: .fs-6 .fw-300 }

{{ site.staffersnobio }}

[syllabus]: syllabus
[piazza]: https://piazza.com/ucsd/spring2026/dsc80
[gradescope]: https://www.gradescope.com/courses/1289847
[github]: https://github.com/dsc-courses/dsc80-2026-sp
[welcome-survey]: https://forms.gle/WoqChddkJZUiTP1v6
[exam-accommodations]: https://forms.gle/n53ZJc2vQYhD7ZKv6
<!-- [Jump to the current week](#week-9-modeling-in-practice){: .btn } [Lab Solutions](https://edstem.org/us/courses/51951/discussion/4183397){: .btn .btn-green } -->

[Podcasts](https://podcast.ucsd.edu/){: .btn }
[Welcome Survey][welcome-survey]{: .btn }
[Exam Accommodations Form][exam-accommodations]{: .btn }


<!-- [Exam Accommodations Form][exam-accommodations]{: .btn }
[Extension Request Form][extension-request-form]{: .btn } -->

<!-- Click the 🎥 button to view the recording of a lecture/discussion.<br>Click the 📝 button to view lecture notebooks after they've been filled in during lecture. -->

<!-- {: .green }
**Welcome to DSC 80! 👋 Make sure to: read the [syllabus][syllabus], check that you can access [Gradescope][gradescope] and [Ed][ed], fill out the [Welcome Survey][welcome-survey], and fill out the [Exam Accommodations Form][exam-accommodations] if you have an exam conflict.** -->

{% for module in site.modules %}
{{ module }}
{% endfor %}
