# Resume tailoring research

Research checked on 2026-09-30. These notes explain the content rules in `SKILL.md`; they are not a checklist to run for every application. Recheck sources when a decision depends on current employer policy or a live posting.

The intended setting is an English-language industry resume, especially for C++ work. Academic CVs and country-specific conventions may differ. ATS optimization is outside this skill's default scope at the user's request. Keeping the existing template is a workflow choice, not a claim that any template has universal parsing guarantees.

## What the evidence supports

### Support an initial scan and a closer read

The [2012 Ladders report](https://www.bu.edu/com/files/2018/10/TheLadders-EyeTracking-StudyC2.pdf), PDF pages 2-4, describes 30 recruiters and roughly six seconds for an initial fit/no-fit decision. The [2018 update](https://www.theladders.com/static/images/basicSite/pdfs/TheLadders-EyeTracking-StudyC2.pdf) reports a 7.4-second initial screen. These are commercial research reports, not a universal time limit or a representative study of C++ hiring. Do not attribute the 2012 sample size to the 2018 study.

A [2023 study of computer-science resume screening](https://www.mdpi.com/2504-4990/5/3/38) recruited 221 recruiters. Longer viewing, particularly of experience, was associated with progression. Its authors acknowledged limited geographic coverage and limited actionable formatting conclusions. Association does not mean that making a resume longer causes more interviews.

[The Tech Resume Inside Out's hiring-pipeline chapter](https://thetechresume.com/samples/the-hiring-pipeline) also describes an initial scan followed by more detailed reading when a candidate appears promising. This is practitioner guidance, not a controlled experiment.

The operational recommendation is to make fit recognizable quickly while retaining credible detail. There is no evidence-based rule that all content must be absorbed in 20 seconds.

### Clear writing can help, but no bullet formula is proven optimal

[Van Inwegen, Munyikwa, and Horton](https://arxiv.org/html/2301.08083v1) report a randomized experiment involving approximately 481,000 online-platform entrants. Algorithmic writing assistance produced an 8% relative increase in hiring probability. The intervention addressed writing quality such as spelling, grammar, and clarity.

This was an online labor market with profile text, not an experiment comparing corporate C++ resumes, keyword counts, or achievement-bullet formulas. It supports improving clarity without changing the underlying facts. It does not justify adding accomplishments, elaborate prose, or invented numbers.

### Select relevant accomplishments and explain the contribution

Several independent practitioner sources agree on these recommendations:

- [Amazon recruiter guidance](https://www.aboutamazon.com/news/workplace/amazon-job-application-resume-writing-tips) recommends simple language, relevant accomplishments, and quantification when possible. It explicitly acknowledges that not every bullet has a quantitative measure.
- [Epic career guidance](https://www.epicgames.com/site/earlycareers/career-paths) recommends clear focus, truthful proficiency claims, prioritizing relevant work, and explaining the applicant's contribution to group projects. It values demonstrable C++ projects for programming applicants.
- [MIT resume guidance](https://capd.mit.edu/resources/resumes/) recommends selecting evidence against the position description, naming relevant technologies within experience descriptions, and documenting accomplishments rather than only responsibilities.
- [Orosz's common-mistakes chapter](https://thetechresume.com/samples/common-mistakes) discusses internal jargon, generic claims, excessive verbosity, and links that do not add useful evidence.

These are well-aligned employer and practitioner recommendations. They do not establish an experimentally optimal bullet length, section order, or resume length. Choose those based on the candidate and role. Content selection and ordering are often more useful than cosmetic verb substitutions.

## C++ role differences

These employer sources illustrate why the skill should identify the engineering domain before choosing evidence. They span different seniority levels and are not a statistical sample or a universal qualification checklist.

- [HRT C++ software engineer](https://www.hudsonrivertrading.com/hrt-job/software-engineer-c/): advanced C++, UNIX/Linux, processor performance, networking, debugging, latency and throughput.
- [Tesla embedded charging firmware](https://www.tesla.com/en_PR/careers/search/job/sr-embedded-software-engineer-charging-236667): C/C++, RTOS, multithreading, peripheral interfaces, hardware bring-up, and unit/SIL/HIL testing.
- [NVIDIA CUDA C++ core libraries](https://nvidia.wd5.myworkdayjobs.com/en-US/NVIDIAExternalCareerSite/job/Senior-Software-Engineer--CUDA-C---Core-Libraries_JR2021114): modern C++, templates, generic programming, parallel algorithms, profiling, API/ABI compatibility, and production libraries. The posting's [public Workday data](https://nvidia.wd5.myworkdayjobs.com/wday/cxs/nvidia/NVIDIAExternalCareerSite/job/Senior-Software-Engineer--CUDA-C---Core-Libraries_JR2021114) provided its text when the rendered page did not.
- [Arm LLVM/compiler engineering](https://careers.arm.com/job/budapest/senior-software-engineer-llvm-compilers/33099/101091132816): LLVM contributions and reviews, optimization, architecture, performance analysis, and technical influence.
- [Epic programming guidance](https://www.epicgames.com/site/earlycareers/career-paths): practical C++, Unreal familiarity, CS fundamentals, and specialization-specific projects.

Use the supplied posting as the authority for a particular application. Do not import requirements from these examples. Preserve distinctions between adjacent kinds of experience, such as general C++ and real-time firmware, or using a GPU library and implementing kernels.

## Resume examples reviewed

These were inspected as examples of presentation and evidence, not as proof that a particular resume caused a successful hiring outcome. Public documents can change.

- [Jake's Resume template](https://www.overleaf.com/latex/templates/jakes-resume/syzfjbzwjncs.pdf), PDF page 1: familiar hierarchy and technologies attached to projects. Its sample bullets are not automatically ideal for C++ roles. Lines of code alone do not establish engineering value.
- [Sunho Kim](https://sunho.io/resume.pdf), PDF page 1: specific compiler and graphics work, including Clang parsing, JIT infrastructure, Vulkan rendering, and recompilers. The useful pattern is domain evidence attached to actual contributions.
- [Ramkumar Ramachandra](https://artagnon.com/resume.pdf), PDF pages 1-2: a clear compiler specialization, named optimization work, upstream contributions, and technical leadership. Useful engineering outcomes need not all be expressed as revenue or percentages.
- [Orosz's original guide](https://thetechresume.com/A_Good_Tech_Resume.pdf), PDF pages 10-13: before/after examples of accomplishments and role-specific emphasis. Rewrites introduce details not present in the shorter originals. In live use, those facts must come from the user; the examples do not license invention.

## Worked accuracy example

Suppose the user supplies these facts:

- Used C++20 for a personal Linux service.
- Used `perf` to identify contention around a shared mutex.
- Changed that synchronization path.
- At the same 5,000 requests/s load-test workload, p99 latency fell from 12 ms to 8 ms.

A supported bullet is:

> Reduced p99 latency from 12 ms to 8 ms in a personal Linux C++20 service by revising shared-mutex synchronization, measured at 5,000 requests/s in load testing.

It does not establish production traffic, real-time guarantees, revenue impact, or a lock-free implementation. Do not add those claims for a posting that asks for them.

If measurements were not supplied, a narrower bullet could describe profiling and revising the synchronization path. Do not invent a percentage, claim lower latency without evidence, or insert a metric placeholder. Ask about outcomes only when the answer would materially improve the revision.

## Limits of resume optimization

[Ashby's referral analysis](https://www.ashbyhq.com/talent-trends-report/reports/referrals) covered 38 million applications across 93,000 jobs and found different progression rates by application source. This is observational data with selection effects, not a causal estimate of the value of a referral.

Resume wording is only one influence on outcomes. Role fit, eligibility, competition, application timing, and recruiting decisions also matter. Do not guarantee interviews or interpret every rejection as evidence that the resume needs another rewrite. It is valid to recommend no change when the relevant evidence is already clear.
