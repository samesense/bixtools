FROM ubuntu:18.04

ENV SNPEFF_VERSION 4_3t
ENV HTSLIB_VERSION 1.9
ENV LOFTEE_VERSION 1.0.2
ENV WGSA_DIR /WGSA

RUN apt update -y && apt upgrade -y && apt install git apt-utils cpanminus build-essential automake mysql-client curl libssl-dev wget pigz openssl libexpat1-dev libmysqlclient-dev unzip wget openjdk-11-jdk zlib1g-dev libncurses5-dev libbz2-dev liblzma-dev libcurl4-openssl-dev -y
RUN cpanm --notest LWP::Simple DBI DBD::mysql Archive::Zip Archive::Extract HTTP::Tiny Test::Simple File::Copy::Recursive Perl::OSType Module::Metadata version TAP::Harness CGI Encode CPAN::Meta JSON DBD::SQLite Set::IntervalTree Archive::Tar Time::HiRes Module::Build Bio::Root::Version
RUN mkdir ${WGSA_DIR} 
RUN cd ${WGSA_DIR} && mkdir htslib && cd htslib && wget https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2 && tar -xjf htslib-${HTSLIB_VERSION}.tar.bz2 && rm htslib-${HTSLIB_VERSION}.tar.bz2 \
&& cd htslib-${HTSLIB_VERSION} && make prefix=/usr/ install
RUN cd /WGSA && mkdir snpeff && cd snpeff && wget -q https://sourceforge.net/projects/snpeff/files/snpEff_v${SNPEFF_VERSION}_core.zip/download && unzip download && rm download
RUN cd ${WGSA_DIR} && wget http://web.corral.tacc.utexas.edu/WGSAdownload/WGSA08.class && mkdir resources && cd resources && wget -r --no-parent http://web.corral.tacc.utexas.edu/WGSAdownload/resources/javaclass/ \
&& mv web.corral.tacc.utexas.edu/WGSAdownload/resources/javaclass ./ && rm -rf web.corral.tacc.utexas.edu
RUN apt remove curl wget git -y && apt autoclean -y &&  apt autoremove -y
