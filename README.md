# nexus-script-api
An API repository with useful scripts to update/ create/ get nexus repository 

## Create a RAW helm repository
**inputs: repository name**
```
{
"name": "helm-repo",
"type": "groovy",
"content": "import org.sonatype.nexus.repository.Repository; import org.sonatype.nexus.repository.storage.WritePolicy; blobStore.createFileBlobStore('project-helm-repo', 'project-helm-repo'); repository.createRawHosted('project-helm-repo', 'project-helm-repo', false, WritePolicy.ALLOW)"
}
```
## Create a docker Repository
inputs: repository name, a HTTP port
```
{
"name": "docker-repo",
"type": "groovy",
"content": "import org.sonatype.nexus.repository.Repository; import org.sonatype.nexus.repository.storage.WritePolicy; blobStore.createFileBlobStore('project-docker-repo', 'project-docker-repo'); repository.createDockerHosted('project-docker-repo', {{PORT_NUMBER}}, 0, 'project-docker-repo', true, true, WritePolicy.ALLOW)"
}
```
## Create a maven repository
```
{
"name": "maven-repo",
"type": "groovy",
"content": "import org.sonatype.nexus.repository.Repository; import org.sonatype.nexus.repository.storage.WritePolicy; import org.sonatype.nexus.repository.maven.VersionPolicy; import org.sonatype.nexus.repository.maven.LayoutPolicy; blobStore.createFileBlobStore('project-maven-repo', 'project-maven-repo'); repository.createMavenHosted('project-maven-repo', 'project'-maven-repo, true, VersionPolicy.repo, WritePolicy.ALLOW_ONCE, LayoutPolicy.STRICT)"
}
```
## Create a maven group
```
{
"name": "maven-group",
"type": "groovy",
"content": "import org.sonatype.nexus.repository.Repository; blobStore.createFileBlobStore('project-maven-group', 'project-maven-group'); repository.createMavenGroup('project-maven-group', ['maven-central', 'project-maven-repo'], 'project-maven-group')"
}
```
## Update a docker group by adding new pository to it
```
{
"name": "setdockergroup",
"type": "groovy",
"content": "import org.sonatype.nexus.repository.config.Configuration; Configuration groupRepoConfig = repository.repositoryManager.get('ms-docker-group').configuration.copy();groupRepoConfig.attributes['group']['memberNames']=groupRepoConfig.attributes['group']['memberNames'] << 'project-docker-repo'; repository.repositoryManager.update(groupRepoConfig)"
}
```

