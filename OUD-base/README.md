docker build --rm=true -t abdi/oud-base  .
docker run -i -t  --name oud1  abdi/oud-base /bin/bash
