###NORMAL e.spirov

##Project structure
.
├── mongo
│   ├── mongo_dep.yaml
│   └── mongo_srv.yaml
├── README.md
└── webapp
    ├── js_cmap.yaml
    ├── js_dep.yaml
    └── js_srv.yaml

##Concept
JS WEBAPP listen connection on 30111;
Mongo waits connections on 20017 from JS;
JS WEBAPP transfer connections to Mondo and counts it into dbtest/vists.

##Installation
git clone https://github.com/espirov/k8s.git
cd k8s/normal && kubectl apply -f mongo/ -f webapp/

##Check
#where counts of curl must be equal number that returns db.visits.countDocuments()
mongosh mongodb://root:example@localhost:27017
use testdb
db.visits.countDocuments()
db.visits.find().pretty()
curl localhost:30111
kubectl -n normal exec -it deploy/mongodb -- bash
mongosh mongodb://root:example@localhost:27017
use testdb
db.visits.countDocuments()
