node {
def mvnHome
stage('Git')   {
git 'https://github.com/khatilov/jenkins.git'
mvnHome = tool 'Maven_3.5.0'
               }
stage('Maven') {
if (isUnix()) {sh "'${mvnHome}/bin/mvn' clean compile findbugs:findbugs pmd:pmd pmd:cpd checkstyle:checkstyle"}
else       {bat(/"${mvnHome}\bin\mvn" clean compile pmd:pmd pmd:cpd findbugs:findbugs checkstyle:checkstyle/)}
               }
stage('PMD')         {step([$class: 'PmdPublisher', pattern: '**/pmd*.xml'])}
stage('Checkstyle')   {step([$class: 'CheckStylePublisher', pattern: '**/checkstyle*.xml'])}
stage('Findbugs')     {step([$class: 'FindBugsPublisher', pattern: '**/findbugs*.xml'])}
stage('CPD')         {step([$class: 'DryPublisher', pattern: '**/cpd.xml'])}
}
