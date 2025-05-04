is a platform to program workflows of data pipeline
> Other options are 
-  Luigi, 
-  SSIS 
-  or Simple Bash scripting 

### DAGs (Directed Acyclic Graph) (Connected Component)
```bash
airflow tasks test etl_pipeline download_file 2023-01-08
```
### ERP(Enterprise Resource Planing System)

### ETL(Extract, Transform, Load) vs ELT(Extract, Load, Transform)

Airflow offers several advantages over using common tools like bash or a combination of other tools for workflow orchestration and scheduling:

1. **Dynamism and Flexibility**: Airflow allows you to define workflows as code, which provides flexibility and dynamism in creating, scheduling, and monitoring complex workflows. With bash scripts or a combination of other tools, managing dependencies and dynamic workflows can become cumbersome.
    
2. **Dependency Management**: Airflow manages dependencies between tasks, ensuring that tasks are executed in the correct order based on their dependencies. This makes it easier to handle complex workflows with interdependent tasks, which can be challenging with bash scripts or manual tool combinations.
    
3. **Monitoring and Logging**: Airflow provides built-in monitoring and logging capabilities, allowing you to track the progress of workflows, view task logs, and easily troubleshoot issues.
    
4. **Scalability**: Airflow is designed to handle large-scale workflow orchestration, allowing you to scale your workflows as your needs grow. It supports distributed execution and can integrate with various execution environments, such as Kubernetes and Apache Mesos. Bash scripts and other common tools may lack the scalability required for complex workflows and large datasets.
    
5. **Workflow Visualization**: Airflow provides a web-based user interface for visualizing and monitoring workflows, which can be helpful for understanding workflow dependencies, identifying bottlenecks, and optimizing performance. This visualization is often lacking or requires manual effort when using bash scripts or other common tools.
    
6. **Extensibility and Integration**: Airflow is highly extensible and integrates with a wide range of third-party tools and services, including databases, cloud platforms, and messaging systems. This allows you to leverage existing tools and infrastructure within your workflow pipelines easily. While you can integrate other tools with bash scripts, Airflow's native integrations streamline the process.