FROM debian:jessie-slim
MAINTAINER Daniele Dalla Torre <dallatorre.daniele@gmail.com>
# install necessary packages
RUN 	apt-get -y update \
	&& apt-get install --no-install-recommends -y \
	ca-certificates \
	make \
	cmake \
	gcc \
	g++ \
	git \
	libgomp1 \
	&& mkdir data \
	&& git clone https://github.com/ftt01/Stormwater-Management-Model.git \
	&& cp Stormwater-Management-Model/docker/outputRead.py /\
	&& cd Stormwater-Management-Model/src/ \
	&& make \
	&& cp ./swmm5 / \
# launch the engine of swmm5	
#ENTRYPOINT ["/bin/bash", "-c", "./swmm5 data/$0.inp data/$0.rpt data/$0.out"]
# purge not needed stuff
	&& apt-get -y remove --purge \
	ca-certificates \
	make \
	cmake \
	gcc \
	g++ \
	git \
	&& apt-get -y autoremove --purge \
	&& cd / \
	&& rm -r Stormwater-Management-Model \
	&& apt-get install --no-install-recommends -y python3
# launch the engine of swmm5	
ENTRYPOINT ["/bin/bash", "-c", "./swmm5 data/$0.inp data/$0.rpt data/$0.out && cp outputRead.py ./data && cd data && python3 outputRead.py $0.out $0 && rm outputRead.py"]
#ENTRYPOINT ["/bin/bash", "-c", "cd data && python3 outputRead.py $0.out $0"]
#CMD	["python3", "outputRead.py $0.out $0"]
