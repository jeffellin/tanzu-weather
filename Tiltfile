load('.tanzu/tanzu_tilt_extensions.py', 'tanzu_k8s_yaml')


SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", default='registry.gcp.ellin.net/tapb3/tanzu-weather')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')

custom_build('registry.gcp.ellin.net/tapb3/tanzu-weather',
    "tanzu apps workload apply -f config/workload.yaml --live-update \
      --local-path " + LOCAL_PATH + " --source-image " + SOURCE_IMAGE + " --yes && \
    .tanzu/wait.sh tanzu-weather",
  ['WeatherForecast.cs'],
  live_update = [
    sync('WeatherForecast.cs', '/workspace/WeatherForecast.cs')
  ],
  skips_local_docker=True
  
)
allow_k8s_contexts('tap-beta3-admin@tap-beta3')
tanzu_k8s_yaml('tanzu-weather', 'registry.gcp.ellin.net/tapb3/tanzu-weather', './config/workload.yaml')
