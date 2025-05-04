### Plugins vs Apply

The `plugins` block is the newer method of applying plugins, and they must be available in the [Gradle plugin repository](http://plugins.gradle.org/). The `apply` approach is the older, yet more flexible method of adding a plugin to your build.

The new `plugins` method does not work in multi-project configurations (`subprojects`, `allprojects`), but will work on the build configuration for each child project.

I would think that as functionality progresses, the `plugins` configuration method will overtake the older approach, but at this point both can be and are used concurrently.



### Build Issue Stuck for 20-30minutes
When `gradlew clean build` gets stuck for a long time (20-30 minutes) in CentOS, there are several possible reasons and troubleshooting steps you can take to resolve the issue:

### 1. **Check for Network Issues (Proxy/Firewall)**

- **Gradle Downloads Dependencies**: If the build is stuck while downloading dependencies, there could be network issues, such as slow connections or blocked access to external repositories.
    - **Solution**: Verify that your network allows access to the required repositories. You can try running `gradlew build --offline` if the dependencies have already been downloaded before.

### 2. **Gradle Daemon Issue**

- **Gradle Daemon**: Sometimes, the Gradle daemon can become unstable, leading to long build times.
    - **Solution**: Try disabling the Gradle daemon and running the build again:
    
    - `./gradlew clean build --no-daemon`

### 3. **Memory/Resource Limitations**

- **Low System Resources**: If the system is running low on memory or CPU, Gradle might get stuck or slow down significantly.
    - **Solution**: Monitor system resources using `top` or `htop` to check if the machine is under heavy load. You can allocate more memory to Gradle by editing the `gradle.properties` file:
    
        `org.gradle.jvmargs=-Xmx2048m`
        
    - Alternatively, kill any idle Gradle daemons using:
        `./gradlew --stop`
        

### 4. **Locking Issues with Gradle Caches**

- **Corrupted or Locked Caches**: Sometimes, Gradle caches can become corrupted or locked, leading to build delays.
    - **Solution**: Clear the Gradle cache by deleting the `.gradle` directory in your project and running the build again:
        

        `rm -rf ~/.gradle/caches/ ./gradlew clean build`
        

### 5. **Suboptimal Disk I/O**

- **Slow Disk I/O**: Gradle builds can be I/O intensive, and if the system’s disk performance is slow, the build will take longer.
    - **Solution**: Ensure there is sufficient disk space and that the disk is not under heavy I/O load. You can monitor disk usage using `iostat` or `iotop`.

### 6. **Gradle Version Issue**

- **Gradle Version Compatibility**: Some versions of Gradle might have known performance issues or might not be fully compatible with the specific project setup.
    - **Solution**: Try upgrading or downgrading Gradle. You can specify the version in `gradle-wrapper.properties` or manually update the Gradle wrapper:
        
        `./gradlew wrapper --gradle-version x.x.x`
        

### 7. **Firewall or Antivirus Interference**

- **Security Software**: In some environments, firewalls or antivirus software may slow down the build by scanning files or blocking certain network traffic.
    - **Solution**: Check for any firewall or antivirus software that might be scanning or interfering with the build process. Temporarily disabling such software may help diagnose the issue.

### 8. **Dependency Resolution Time**

- **Slow Dependency Resolution**: Sometimes the process of resolving dependencies from external repositories may take longer, especially if there are multiple repositories or slow connections.
    - **Solution**: You can try setting a higher logging level to identify which part of the build process is causing the delay:
        
        `./gradlew clean build --info ./gradlew clean build --debug`
        

### 9. **Daemon Logs**

- **Check Daemon Logs**: Gradle stores daemon logs in the `~/.gradle/daemon/<gradle_version>/` directory, which might provide clues about what's going wrong.
    - **Solution**: Review the logs in this directory to check for errors or unusual behavior.

If these suggestions don't help narrow down the issue, reviewing the specific part of the build that is hanging or sharing the build logs could provide more insight.