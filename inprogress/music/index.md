---
layout: page
title:  "Musicology and Ethnomusicology"
---

## Musicology and Ethnomusicology

- [Conferences](#conferences)

- [Publishing](#publishing)

- [Granting](#granting)


## Conferences 

Currently have (see below):
- Statistics on non-affiliated paper presentations at the three major musicology conferences (including SMT when inextricable from large data)

Need:
- Statistics on IASPM and other music conferences, like Jazz-specific conferences
- Would ideally like any possible statistics on amount of non-affiliated scholars that submit papers to conferences


### Number of independent/non-affiliated scholars presenting papers at conferences (see note):
 <pre class="mermaid">
            graph TD
            A[SAM] 
            A--> B[2017]
            A--> C[2018]
            A--> D[2019]
            A--> E[2020]
            A--> F[2021]
            A--> G[2022]
            B-->BB[2/145, 1.38%]
            C-->CC[2/137, 1.46%]
            D-->DD[3/160, 1.88%]
            E-->EE[2/111, 1.80%]
            F-->FF[7/120, 5.83%]
            G-->GG[5/81, 6.17%]

    </pre>

<pre class="mermaid">
            graph TD
            A[SEM] 
            A--> B[2017]
            A--> C[2018]
            A--> D[2019]
            A--> E[2020]
            A--> F[2021]
            A--> G[2022]
            B-->BB[8/312, 2.56%]
            C-->CC[4/299, 1.34%]
            D-->DD[9/376, 2.39%]
            E-->EE[2/375, .0.53%]
            F-->FF[4/340, 1.18%]
            G-->GG[MusicCon22: 12/746, 1.61%]

</pre>

<pre class="mermaid">
            graph TD
            A[AMS] 
            A--> B[2017]
            A--> C[2018]
            A--> D[2019]
            A--> E[2020]
            A--> F[2021]
            A--> G[2022]
            B-->BB[10/286, 3.50%]
            C-->CC[14/415, 3.37% *]
            D-->DD[18/344, 5.23%]
            E-->EE[3/278, 1.08%]
            F-->FF[9/286, 3.15%]
            G-->GG[MusicCon22: 12/746, 1.61%]


</pre>

\* Includes SMT


### Notes: 
- Statistics only include papers presented. Chairs, roundtables, special interest groups, posters, etc., are not included.

## Publishing 

Currently have:
- All music titles from 2017–2023 from:
  - Duke University Press
  - Oxford University Press
  - University of Chicago Press
  - University of North Carolina Press
  - University of Michigan Press
  - University of California Press
  - University of Mississippi Press
  - University of Illinois Press
  - MIT Press
  - Indiana University Press

Analyzing # of TT and non-affiliated and North American authors

### Breakdown of authors, combined
<pre class="mermaid">
  pie
  "Tenured or TT (517/641)" : 517
  "No affiliation, non-PhD (94/641)" : 94
  "Institutional affiliation, non-TT (23/641)" : 23
  "PhD holder, no affiliation (7/641)" : 7
</pre>

## Key
Tenured or TT (517/641): 81%

No affiliation, non-PhD (94/641): 15%

Institutional affiliation, non-TT (23/641): 4%

PhD holder, no affiliation (7/641) : 1%

Looking for:
- Number of journal articles in the top journals published by non-affiliated scholars in the past 5 years
- Alternative publication methods both for non-affiliated and affiliated scholars

## Granting 

Looking for:
- Number of grant opportunities specifically for non-affiliated scholars
- Number of non-affiliated scholars who are awarded the major music association-funded grants
- Number of non-affiliated scholars who are awarded state-wide humanities funded grants
- Number of non-affiliated scholars who are awarded federal humanities and arts funded grants


<script type="module">
      import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@9/dist/mermaid.esm.min.mjs';
      mermaid.initialize({ 
        startOnLoad: true,         
        // theme: 'neutral',
         fontFamily: 'Bitter, sans-serif',
         fontSize: '15px'


      });
    </script>

 <button onclick="topFunction()" id="myBtn" title="Go to top"><span class="material-symbols-outlined">
vertical_align_top
</span></button>

<script>
	// Get the button:
let mybutton = document.getElementById("myBtn");

// When the user scrolls down 20px from the top of the document, show the button
window.onscroll = function() {scrollFunction()};

function scrollFunction() {
  if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
    mybutton.style.display = "block";
  } else {
    mybutton.style.display = "none";
  }
}

// When the user clicks on the button, scroll to the top of the document
function topFunction() {
  document.body.scrollTop = 0; // For Safari
  document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
}
</script>