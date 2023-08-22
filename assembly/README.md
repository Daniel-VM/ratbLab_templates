# Guide to run a wgs analysis

## STEPS
0. Copy the wgs repo template into /data/cnm/ratb/services/ratblab/[wgs_service_name]

```shell
cp -r /data/cnm/ratb/templates/assembly /data/cnm/ratb/services/ratblab/[wgs_service_name]
```

1. Create a soft link from /srv/fastq_repo/ to RAW_NC/

```shell
cd RAW_NC/
find /srv/fastq_repo/[RUN-NAME] -type f -name "*.fastq.gz" -exec ln -s {} . \;
```

2. Run the lablog in ANALYSIS. 

```shell
cd ANALYSIS/
bash lablog_assembly
```

3 Run the ANALYSIS/WGS_ANALYSIS/lablog 

```shell
cd ASSEMBLY01/
bash lablog
```

3. Copy service to sftp
```shell
srun --partition short_idx rsync -rlv /data/cnm/ratb/services/ratblab/[service_name] /scratch/cnm/antibioticos
```

3. Deploy analysis
```shell
cd  /scratch/cnm/antibioticos/[service_name]/ANALYSIS/${date}_ASSEMBLY01
sbatch assembly.batch
```
