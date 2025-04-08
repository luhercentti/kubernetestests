
update manifest, go to folder base, then overlays/dev or prod and run to update manifest:
kustomize edit fix .

to apply :
kubectl apply -k overlays/dev/

kubectl apply -k overlays/prod/