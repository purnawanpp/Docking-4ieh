# Docking-3htb Using Vina forcefield
Tutorial Docking Menggunakan Autodock Vina versi 1.2.3 (2021)

# Perangkat lunak yang dibutuhkan 
1. Vina.exe (Version 1.2.3) download disini https://github.com/ccsb-scripps/AutoDock-Vina/releases/download/v1.2.3/vina_1.2.3_windows_x86_64.exe, vina_1.2.3_windows_x86_64.exe ubah namanya menjadi vina.exe
2. ADFR Tools (Version 1.2) https://ccsb.scripps.edu/adfr/download/1067/
3. Mgl Tools (Version 1.5.7) https://ccsb.scripps.edu/download/262/
4. Avogadro (Version 1.2) https://sourceforge.net/projects/avogadro/files/latest/download
5. Discovery Studio (Version 2022) https://discover.3ds.com/discovery-studio-visualizer-download
6. Marvin Sketch (Version 2022) https://chemaxon.com/products/marvin/download cara install marvin sketch https://www.researchgate.net/profile/Purnawan-Pontana-Putra/publication/356913436_Tutorial_Installing_Marvin_Sketch_Software_and_Using_SWISS_ADME/links/61b2b2ee590a0b7ed6346b1a/Tutorial-Installing-Marvin-Sketch-Software-and-Using-SWISS-ADME.pdf
7. Windows terminal https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701

# Cara mengetahui active site dan binding sitenya
1. Baca artikel proteinnya
2. Menggunakan aplikasi Uniprot https://www.uniprot.org/
3. Menggunakan aplikasi Discovery Studio, 
4. Menggunakan aplikasi server online seperti: ICM-PocketFinder, CASTp, Chimera, Qsite, Scfbio online server

# Pemisahan ligand dan protein (Menggunakan Biovia Discovery Studio)
1. Pisahkan Protein, buang air dan ligannya
2. Pisahkan ligand, buang protein, air 

# Preparasi Protein (Menggunakan Autodock Tools)
1. Dipisahkan air dan ligannya terlebih dahulu menggunakan Biovia Discovery Studio
2. Klik File Read Molecules cari protein.pdb
3. Dilakukan penambahan Hidrogen dengan Edit-Add Hidrogen-All
4. Edit tambahkan muatan gasteiger
5. Edit-Hidrogen Merge Non Polar
6. Grid-Macromolecules-Choose
7. save protein.pdbqt

# Preparasi Ligand (Menggunakan Autodock Tools)
1. Klik File Read Molecules cari ligand.pdb
2. Dilakukan penambahan Hidrogen dengan Edit-Add Hidrogen-All
3. Edit tambahkan muatan gasteiger
4. Edit-Hidrogen Merge Non Polar
5. Ligand-Input-choose
6. Pilih ligand.pdb
7. ligand-Toorsion tree-detect root
8. ligand-output-save as ligand.pdbqt

# Perintah di terminal untuk mengetahui Grid Box menggunakan Autogrid (Menggunakan Terminal)
1. python.exe prepare_gpf.py -l 4ieh_ligand.pdbqt -r 4ieh_protein.pdbqt -y
2. autogrid4 -p 4ieh_protein.gpf -l 4ieh_protein.glg

# Buat File GridBoxnya (Mengunakan Notepad) 
1. Buka file dengan 4ieh_protein.gpf
2. Catat npts 41 40 40 sebagai size x, y, z
3. Catat gridcenter -0.004 -0.187 0.078 sebagai center x, y, z
4. Buat file grid.txt didalamnya tertulis: 
center_x = -0.004
center_y = -0.187
center_z = 0.078
size_x = 40
size_y = 40
size_z = 40
5. Contoh file grid.txt dapat dilihat disini https://github.com/purnawanpp/Docking-3htb/blob/main/grid.txt

# Prosedur Docking (Menggunakan Terminal)
1. vina --receptor 4ieh_protein.pdbqt --ligand 4ieh_ligand.pdbqt --config grid.txt --exhaustiveness=8 --out 4ieh_ligand_vina_out.pdbqt > results.txt
2. vina_split --input 4ieh_ligand_vina_out.pdbqt

# Perhitungan nilai RMSD (Menggunakan Biovia Discovery Studio)
1. Buka file 4ieh_ligand.pdbqt
2. Drag file 4ieh_ligand_vina_out_ligand_1.pdbqt
3. Klik File 4ieh_ligand.pdbqt,
4. Klik Structure-RMSD-Set Reference
5. Klik File 4ieh_ligand_vina_out_ligand_1.pdbqt
6. Klik Structure-RMSD-Heavy Atoms
7. Dibagian bawah nanti kelihatan nilai RMSDnya, nilai RMSD yang disarankan adalah <2

# Optimasi Geometri (Avogadro)
1. Buka Avogadro
2. Klik File-open-ligand/obat dengan format .mol2
3. Klik Extension-Molecular Mecahanics-Setup Force Field
4. Pilih setup Force-Field pilih UFF 
5. Klik Extension-Pilih-Optimize Geometry
