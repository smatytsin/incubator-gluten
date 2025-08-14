export HADOOP_HOME=/hadoop
git clone --depth 1 --branch branch-1.4_spark3.5.7 https://github.com/smatytsin/incubator-gluten.git /work14_spark3.5.7
export DEPENDENCY_DIR=/work/build-deps
source /opt/rh/gcc-toolset-11/enable
cd /work14_spark3.5.7
export NUM_THREADS=12
./dev/builddeps-veloxbe.sh --enable_vcpkg=ON --build_arrow=OFF --build_tests=OFF --build_benchmarks=OFF --enable_s3=ON --enable_gcs=OFF --enable_hdfs=ON --enable_abfs=OFF --run_setup_script=OFF 2>&1 | tee build2.log

mvn clean package -Pbackends-velox -Pspark-3.5 -DskipTests


./dev/builddeps-veloxbe.sh build_velox


