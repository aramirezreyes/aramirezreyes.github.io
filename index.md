@def title = "Argel Ramírez Reyes"

<!-- -----------------
     BIOGRAPHY SECTION
     ----------------- -->

\begin{section}{name="about"}

<!-- RIGHT COLUMN -->
@@col-12,col-lg-4,profile

\img{"/assets/img/perfil_sq.jpeg", class="avatar avatar-square", alt="Argel Ramírez Reyes"}
\portrait{
  name="Argel Ramírez Reyes",
  job="Tropical cyclone modeler",
  resume="/assets/ARR_resume.pdf",
  email="argel.ramirez@gmail.com",
  twitter="https://www.threads.net/@hurakandinsky",
  gscholar="https://scholar.google.com/citations?user=JkcQycYAAAAJ&hl=es",
  github="https://github.com/aramirezreyes",
  linkedin="https://www.linkedin.com/in/argelramirezreyes/"
}
@@ <!-- end of column -->


<!-- LEFT COLUMN -->
@@col-12,col-lg-8

\begin{biography}{}
I am interested in tropical cyclones (and other hydro-meteorological phenomena), supercomputing, open science and open software. I am interested in the processes that create tropical cyclones, how they are changing with climate, and how they interact with society to create risk.
\end{biography}

\shortcv{
  interests=["Fluid Dynamics", "Tropical cyclones", "Free software", "Supercomputing", "Climate"],
  education=[
    ("PhD in Atmospheric Science, 2023", "University of California, Davis"),
    ("Masters in Scientific Computing, 2017", "Université de Lille 1, Sciences et Technologies"),
    ("BSc in Physics, 2016", "Universidad Nacional Autónoma de México")]
}

@@ <!-- end of column -->



\end{section}

\begin{section}{name="recent news"}

<!-- --------------
     SHORT PUB LIST SECTION
     -------------- -->


@@col-12,col-lg-6,pubs
 \
\sectionheading{"Recent publications", class="col-md-12"}
{{pub}}

@@


<!-- --------------
     NEWS SECTION
     -------------- -->


@@col-12,col-lg-6,news

 \
\sectionheading{"News", class="col-md-12"}
{{recentnews 3}}

@@
\end{section}



<!-- --------------
     SKILLS SECTION
     -------------- -->

\begin{section}{name="skills", class="wg-featurette", rowclass="featurette"}

\sectionheading{"Favorite tools", class="col-md-12"}

\skill{"Julia", "90%", img="/assets/img/julia-dots-colors.svg"}
\skill{"Emacs", "50%", img="/assets/img/emacsicon.png"}
\skill{"Photography", "10%", fa="camera-retro"}

\end{section}


