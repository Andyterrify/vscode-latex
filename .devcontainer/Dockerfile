FROM ubuntu

RUN echo "Europe/London" > /etc/timezone
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/London

# Set localle
RUN apt update && apt install -y tzdata locales

RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 

# Install required packages
RUN apt update && export DEBIAN_FRONTEND=noninteractive && \
    apt install -y git biber texlive texlive-latex-extra \
    texlive-bibtex-extra texlive-xetex chktex latexmk \
    cpanminus curl make

# Configure latexindent
RUN git clone https://github.com/cmhughes/latexindent.pl.git
ENV PATH=$PATH:/latexindent.pl
## Latexindent perl packages
RUN cpanm --local-lib=~/perl5 local::lib && eval $(perl -I ~/perl5/lib/perl5/ -Mlocal::lib)
RUN curl -L http://cpanmin.us | perl - App::cpanminus
RUN cpanm YAML::Tiny
RUN cpanm File::HomeDir
RUN cpanm Unicode::GCString
RUN cpanm Log::Log4perl
RUN cpanm Log::Dispatch::File
