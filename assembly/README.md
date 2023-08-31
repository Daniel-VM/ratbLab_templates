# Guide to run a wgs analysis

## STEPS
0. Copy the wgs repo template into /data/cnm/ratb/services/ratblab/[wgs_service_name]

```shell
cp -r /data/cnm/ratb/templates/assembly/* /data/cnm/ratb/services/ratblab/[wgs_service_name]
```

1. Create a soft link of raw NGS reads into to RAW_NC/

```shell
cd /data/cnm/ratb/services/ratblab/[wgs_service_name]/RAW_NC/
find /srv/fastq_repo/[RUN-NAME] -type f -name "*.fastq.gz" -exec ln -s {} . \;
```

2. Run the lablog in ANALYSIS to create folder analysis for target reads. 

```shell
cd ANALYSIS/
bash lablog_assembly
```

3 Run the assembly analysis lablog to create:
    - input samplesheet.csv
    - parse workflow parameters
    - setup slurm job

```shell
cd ASSEMBLY01/
bash lablog
```

3. Copy service to sftp
```shell
srun --partition short_idx rsync -rlv /data/cnm/ratb/mperezv/ANALYSIS/[service_name] /scratch/cnm/antibioticos
```

3. Deploy analysis
```shell
cd  /scratch/cnm/antibioticos/[service_name]/ANALYSIS/${date}_ASSEMBLY01
sbatch assembly.batch
```
