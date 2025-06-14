@def title = "Argel Ramírez Reyes"

<!-- -----------------
     BIOGRAPHY SECTION
     ----------------- -->

\begin{section}{name="about"}

<!-- RIGHT COLUMN -->
@@col-12,col-lg-4,profile

\img{"/assets/img/perfil_sq.jpeg", class="avatar avatar-circle", alt="Argel Ramírez Reyes"}
\portrait{
  name="Argel Ramírez Reyes",
  job="Tropical cyclone modeler",
  resume="/assets/ARR_resume.pdf",
  email="argel.ramirez@gmail.com",
  gscholar="https://scholar.google.com/citations?user=JkcQycYAAAAJ&hl=es",
  github="https://github.com/aramirezreyes",
  linkedin="https://www.linkedin.com/in/argelramirezreyes/"
}
@@ <!-- end of column -->


<!-- LEFT COLUMN -->
@@col-12,col-lg-8

\begin{biography}{}
I am a tropical cyclone researcher and an open source enthusiast (in computing and in science). I am interested in the processes that create tropical cyclones, how they are changing with climate, and how they interact with society to create risk. Apart from tropical cyclones (and other hydro-meteorological phenomena), I enjoy thinking about supercomputing, open science and open software.
\end{biography}

\shortcv{
  interests=["Risk", "Tropical cyclones", "Fluid dynamics", "Free software", "Supercomputing", "Climate"],
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

\skill{"Julia", img="/assets/img/julia-dots-colors.svg"}
\skill{"Emacs", img="/assets/img/emacsicon.png"}
\skill{"Photography", fa="camera-retro"}

\end{section}


