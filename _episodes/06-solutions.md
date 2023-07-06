---
title: "Solutions and questions"
teaching: 40
questions:
- "How should I construct selection criteria for a physics analysis?"
objectives:
- "Combine trigger, identification, and isolation information into a full selection for a specific physics process."
keypoints:
- "Triggers usually impose various kinematic restrictions on objects of interest."
- "Final state objects produced promptly from the proton collision are typically required to have significant momentum, tight ID quality, and to be isolated (depending on the topology of the physics process."
- "Veto objects are typically selected using looser criteria so that the efficiency of the veto is very high."
- "Correlations between objects can be used either to select specifically for signal events or reject background events."
---

All of the trigger and physics object information from this lesson is combined when designing the event selection procedure for a physics analysis.

> ## Workshop analysis example: H -> tau tau
> Later in the workshop we will use a search for Higgs bosons as an example analysis. The signal for this search is one Higgs boson that decays to two tau leptons, with one tau lepton decaying hadronically and the other tau lepton decaying to a muon and neutrinos.
{: .callout}

> ## Your analysis example
> What is a physics process that you might study? Let's design a possible CMS event selection. If your process includes a particle with multiple possible decay modes, choose one (or a small group of very similar decay modes) as a test case for this challenge. 
{: .prereq}

For the Higgs search and/or your own process of interest, use the information you have gained about triggers and physics objects to sketch out a possible event selection for your analysis.

> ## Signal
> Which final state particles would you expect to observe in the detector from your "signal" process?
>> ## Solution
>> For the [Higgs -> tau tau search](https://arxiv.org/pdf/1401.5041.pdf) we expect one hadronic tau object, one muon, and MET from the Higgs boson decay, and potentially two or more jets if the Higgs boson was produced via vector boson fusion.
>><img src="http://cms-results.web.cern.ch/cms-results/public-results/publications/HIG-13-004/CMS-HIG-13-004_Figure_001-a.png" alt="Feynman1" width="500"/> <img src="http://cms-results.web.cern.ch/cms-results/public-results/publications/HIG-13-004/CMS-HIG-13-004_Figure_001-b.png" alt="Feynman2" width="500"/>
>{: .solution}
{: .objectives}


Based on these particles, consider:

 * Which trigger or triggers would be useful to make sure your signal events are represented in the dataset?

> ## Solution
> This analysis is perfect for a "cross trigger" that selects more than one object! The trigger used in this example is `HLT_IsoMu17_eta2p1_LooseIsoPFTau20`, requiring both a muon and a tau.
{: .solution}


 * Which objects should you require in each event?

> ## Solution
> Certainly at least 1 muon and 1 hadronic tau!  An analyst targeting VBF production might also require at least 2 jets, especially jets that were detected near the endcaps of the detector. A MET requirement is more tricky to choose: since the neutrinos involved in this event likely do not carry away very large momenta, imposing a MET threshold may not significantly improve the selection.
{: .solution}

 * What kinematic criteria might you requier for each object? (momentum, angular regions, etc)

> ## Solution
> The trigger criterion imposes some constraints: we will lose muons with pT below 17 GeV or large pseudorapidity, and hadronic taus with pT below 20 GeV. Since there is typically some "turn-on" in the efficiency of the trigger selection, it would be safer to add a momentum buffer to our selection. This analysis requires:
> * 1 or more muons with pT > 20 GeV and absolute eta < 2.1
> * 1 or more hadronic taus with pT > 30 GeV and absolute eta < 2.4
{: .solution}

 * What quality criteria might you require for each object? (identification, isolation)

> ## Solution
> Tau selection:
>  * We learned from the tau reference twiki that we should always require `taus_iddecaymode` to be true.
>  * The trigger adds an extra criterion: we should at least require that the `taus_idisoloose` flag is true. In fact, the version of this analysis on the OpenData portal requires that even the `taus_idisotight` flag is true.
>  * We want to protect against selecting taus that were actually misidentified electrons or muons. This is done by requiring `taus_idantieletight` and `taus_idantimutight` to be true.
>
> Muon selection:
>  * The ID is not restricted by the trigger, but the "tight" working point is by far the most popular choice for any signal muons.
>  * Since the muon is not expected to be produced very near to a jet or the tau, this analysis requires that the `muon_pfreliso04all` isolation be < 0.1.
{: .solution}

 * Are there any correlations between your objects that you might exploit?

> ## Solution
> Since the Higgs boson is neutral, we expect that the muon and tau lepton have opposite charges. This requirement can help reduce background events with unassociated muon and tau objects.
{: .solution}

> ## Background
> Which SM backgrounds could easily mimic your signal, given a few extra physics objects, or a few missing physics objects?
>> ## Solution
>> The backgrounds for the Higgs search are described on the [OpenData Portal page](http://opendata.web.cern.ch/record/12350)
>{: .solution}
{: .objectives}

Based on these processes, consider:
 * Which background simulations should you include in your study?

> ## Solution
> The most important sample to include is Z -> tau tau, since the final state is effectively identical to the Higgs boson case. Other Z boson, W boson, and top quark samples will be included. Multijet ("QCD") background simulation is often not used in final results because of the difficulty in modeling pure QCD interactions, so this background is more often estimated using data in alternate selection regions ("control regions").
{: .solution}

 * Should you apply any upper or lower limits on the numbers of certain physics objects in your events?

> ## Solution
> It is often useful to select events with *exactly* a certain number of objects rather than *at least* a certain number. Close study of background versus signal processes in simulation can help show which choices are best for a certain signal. In this case, since muons and tau combinations are rare from proton collisions, we will simply select the best single muon and tau to reconstruct as a Higgs boson rather than imposing limits.
{: .solution}

 * Are there any objects you should *veto* from your events? What quality criteria might you choose?

> ## Solution
> In a sample list consisting of Higgs or Z -> tau tau, Z -> leptons, W -> leptons, and top pairs -> (bW)(bW) -> bb+leptons, one object stands out: b-tagged jets. The top pair background in this analysis can be dramatically reduced by rejecting events with any b-tagged jets. Typically a loose requirement is used on veto objects so that efficiency for rejecting background-heavy events is highest, but this is a case-by-case decision.
>
> In the published analysis, event categories targeting VBF Higgs production vetoed additional jets in the central region of the detector since those are inconsistent with a VBF hypothesis. Events are also categorized based on which leptons (muons or electrons) appear in the event -- if not using multiple categories, a muon analysis might veto on the presence of electrons to reduce backgrounds.
{: .solution}

 * Are there any correlations between objects in background that might be useful for rejection?

> ## Solution
> Looking back to the background list, the W boson background has the unique feature that a single neutrino is expected from its decay products. The transverse mass (see [equation 2](https://arxiv.org/pdf/1401.5041.pdf)) constructed from the muon and MET is typically near the W boson mass for this background, while it should have small values in signal since the muon and the tau-decay neutrinos are not associated. This analysis requires the muon+MET transverse mass to be < 30 GeV to reject W boson background.
{: .solution}

## Prepare for the $$t\bar{t}$$ analysis

For Wednesday, due to the large size of the datasets involved, we need to make a pre-filtering or selection to our data.  In this version of POET we have implemented those modifications and apply two filters.  One on the triggers we will be using and a second one to require at least one *tight* electron or one *tight* muon.  Can you spot these filters in the configuration file?

Let's have a look.

The trigger filter:

~~~
#----------- Turn on a trigger filter by adding this module to the the final path below -------#
process.hltHighLevel = cms.EDFilter("HLTHighLevel",
    TriggerResultsTag = cms.InputTag("TriggerResults","","HLT"),
    HLTPaths = cms.vstring('HLT_Ele22_eta2p1_WPLoose_Gsf_v*','HLT_IsoMu20_v*','HLT_IsoTkMu20_v*'),           # provide list of HLT paths (or patterns) you want
    eventSetupPathsKey = cms.string(''), # not empty => use read paths from AlCaRecoTriggerBitsRcd via this key
    andOr = cms.bool(True),             # how to deal with multiple triggers: True (OR) accept if ANY is true, False (AND) accept if ALL are true
    throw = cms.bool(True)    # throw exception on unknown path names
)
~~~
{: .language-python}

You guessed correctly if thought the included triggers are the ones we are going to use for our $$t\bar{t}$ analysis.

The electron/muon filter:

~~~
#---- Example of a very basic home-made filter to select only events of interest
#---- The filter can be added to the running path below if needed but is not applied by default
process.elemufilter = cms.EDFilter('SimpleEleMuFilter',
                                   electrons = cms.InputTag("slimmedElectrons"),
                                   muons = cms.InputTag("slimmedMuons"),
                                   vertices=cms.InputTag("offlineSlimmedPrimaryVertices"),
                                   mu_minpt = cms.double(26),
                                   mu_etacut = cms.double(2.1),
                                   ele_minpt = cms.double(26),
                                   ele_etacut = cms.double(2.1)
                                   )
~~~
{: .language-python}

Finally, let us just mention that, instead of the `mytriggers` module (which was commented out), we have set up a simpler trigger retriever called `mysinpletrig` in the `poet_cfg.py`.



{% include links.md %}

