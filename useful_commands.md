To find out what data can be printed, run. Can pipe to jq to format
`docker container ls --format='{{json .}}'`

The below command will output a string instead of the defaul list output
`docker container inspect ubuntu-vol-test --format '{{join .HostConfig.ReadonlyPaths ", " }}'`

This will output and format multiple columns along with headings
`docker container ls -a --format "table {{.Command}}\t{{.Names}}"`

This will show just output (not headings) and wont format multiple columns
`docker container ls --format {{.Names}}`
