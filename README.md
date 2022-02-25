# Docking-3htb
Tutorial Docking Menggunakan Autodock Vina versi 1.2.3 (2021)

# Cara mengetahui active site dan binding sitenya
1. Baca artikel proteiinya
2. Menggunakan aplikasi Uniprot https://www.uniprot.org/
3. Menggunakan aplikasi Discovery Studio, 
4. Menggunakan aplikasi server online seperti: ICM-PocketFinder, CASTp, Chimera, Qsite, Scfbio online server

# Using Vina forcefield
Validasi dengan menggunakan Re-Docking

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
4. Buat file grid.txt didalamnya tertulis :
#center_x = -0.004
center_y = -0.187
center_z = 0.078
size_x = 40
size_y = 40
size_z = 40#

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

# Optimasi Geometri (Avogadro)
1. Buka Avogadro
2. Klik File-open-ligand/obat dengan format .mol2
3. Klik Extension-Molecular Mecahanics-Setup Force Field
4. Pilih setup Force-Field pilih UFF 
5. Klik Extension-Pilih-Optimize Geometry
