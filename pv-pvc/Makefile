stage = dev
include ../stages/$(stage)

run: 
	@echo "namespace variable is set to $(namespace)"
	@cat pv-pvc.yaml | sed "s|NAMESPACE|$(namespace)|g" | kubectl apply -f -
	
stop:
	@cat pv-pvc.yaml | sed "s|NAMESPACE|$(namespace)|g" | kubectl delete -f -