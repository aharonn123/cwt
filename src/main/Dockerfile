FROM mlaccetti/docker-oracle-java8-ubuntu-16.04

##### USER root #####
USER root 

EXPOSE 8080


ARG imageName=tomcat 
ARG imageHome=/${imageName}
ARG imageVersion=9.0.8
ARG imageSrcName=apache-${imageName}-${imageVersion}
ARG imageSrc=${imageSrcName}.tar.gz

### Some info for inspection ###
LABEL provider="Nir Aharon" \
			image.name=${imageName} \
			image.version=${imageVersion} \
			image.source=${imageSrc} \
			container.home=${imageHome} 
			

COPY ${imageSrc} ${imageHome}/${imageSrc}

### Prepare account ###
RUN useradd -m --shell /bin/bash --home ${imageHome} ${imageName} && \
		cd ${imageHome} && \
		tar -xf ${imageSrc} && \
		chown -R ${imageName}:${imageName} ${imageHome} && \
		mkdir ${imageHome}/${imageSrcName}/webapps/myApp && \ 
		rm ${imageHome}/${imageSrc}

COPY myApp/ ${imageHome}/${imageSrcName}/webapps/myApp

##### USER ${imageName} #####
USER ${imageName} 
		
ENV CATALINA_HOME=${imageHome}/${imageSrcName} CATALINA_BASE=${imageHome}/${imageSrcName} CATALINA_BIN=${imageHome}/${imageSrcName}/bin PATH=${imageHome}/${imageSrcName}/bin:$PATH


CMD startup.sh ; /bin/bash ; cd