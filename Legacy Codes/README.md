#!/bin/bash
z=0
menu=0 

input(){
            let z=$z+1
            echo -n "No. Antrian		: "
            read nomor[$z]
            echo -n "Nama Kasir	        : "
            read kasir[$z]
            echo -n "Nama Pembeli		: "
            read pembeli[$z]
            echo -n "Pembelian	        : "
            read beli[$z]
            echo -n "Harga 		        : Rp."
            read harga[$z]  
            echo -n "Jumlah     		: "
            read jumlah[$z]
            let total[$z]=${harga[$z]}*${jumlah[$z]}
            echo "Total				    : Rp.${total[$z]}"
            echo "   "
} 
view(){
            for((a=1;a<=z;a++))
            do
			echo "----------------------$a------------------------"
			echo "   "
                        echo "No. Antrian			: ${nomor[$a]}"
                        echo "Nama Kasir			: ${kasir[$a]}"
                        echo "Nama Pembeli			: ${pembeli[$a]}"
                        echo "Pembelian 			: ${beli[$a]}"
                        echo "Harga     			: Rp.${harga[$a]}"
                        echo "Jumlah     			: ${jumlah[$a]}"
                        echo "Total      			: Rp.${total[$a]}"
                        echo "   "
            done
}
search(){
            echo -n "Coba masukkan No. Antrian anda: "
            read cari
            a=0
            b=0
            while [ $a -le $z ] && [ $b == 0 ]
            do
                        let a=$a+1
                        if [ "${nomor[a]}" == $cari ]
                        then
                                    b=1
                        fi
            done
} 
pembayaran(){
	search
	if [ $a -le $z ]
	then
			echo "No. Antrian            			: ${nomor[$a]}"
			echo "  "
                        echo "Nama Pembeli			: ${pembeli[$a]}"
                        echo "Nama Kasir			: ${kasir[$a]}"
                        echo "Pembelian 			: ${beli[$a]}"
                        echo "Harga     			: Rp.${harga[$a]}"
                        echo "Jumlah     			: ${jumlah[$a]}"
                        echo "Total      			: Rp.${total[$a]}"
                        echo "   "
			echo "----------------------------------------------------"
			echo "   "
			echo -n "Bayar                       	: Rp."
			read bayar[$a]
			if [ ${bayar[$a]} -lt ${total[$a]} ]
			then 
			echo "   "
			echo "--------------- Uang anda tidak cukup -------------------"
			elif [ ${bayar[$a]} -eq ${total[$a]} ]
			then
			echo "   "
			echo "----------------- Pembayaran selesai --------------------"
			else
			let kembali[$a]=${bayar[$a]}-${total[$a]}
			echo "   "
			echo -n "Kembalian 	                : Rp.${kembali[$a]}"
			fi
	else
		echo "Data pembelian anda tidak ada,coba lagi :)"	
	fi
}
update(){
            search
            if [ $a -le $z ]
            then
                        echo "-------------------------------------------------"
                        echo "   "
                        echo "Pembelian 			: ${beli[$a]}"
                        echo "Harga     			: Rp.${harga[$a]}"
                        echo "Jumlah     			: ${jumlah[$a]}"
                        echo "Total      			: Rp.${total[$a]}"
                        echo "  "
                        echo "-------------------------------------------------"
            echo "   "
            echo -n "Pembelian 		    : "
            read beli[$z]
            echo -n "Harga     		    : Rp."
            read harga[$z]  
            echo -n "Jumlah    		    : "
            read jumlah[$z]
            let total[$z]=${harga[$z]}*${jumlah[$z]}
            echo "Total     		    : Rp.${total[$z]}"
            echo "   "
            else
                        echo "Data pembelian anda tidak ada,coba lagi :)"
            fi
} 
delete(){
            search
            if [ $a -gt $z ]
            then
                        echo "Data pembelian anda tidak ada,coba lagi :)"
            else
                        while [ $a -lt $z ]
                        do
                                    let b=$a+1
                                    nomor[$a]=${nomor[$b]}
                                    pembeli[$a]=${pembeli[$b]}
                                    kasir[$a]=${kasir[$b]}
                                    beli[$a]=${beli[$b]}
                                    harga[$a]=${harga[$b]}
                                    jumlah[$a]=${jumlah[$b]}
                                    total[$a]=${total[$b]}
                                    let a=$a+1
                        done
                        let z=$z-1
                        echo "Data $cari anda berhasil dihapus"
            fi
} 
cetak(){
            search
            if [ $a -le $z ]
            then
                        echo "-------------------------------------------"
                        echo "   "
                        echo "No. Antrian			: ${nomor[$a]}"
                        echo "Nama Pembeli			: ${pembeli[$a]}"
                        echo "Nama Kasir			: ${kasir[$a]}"
                        echo "Pembelian 			: ${beli[$a]}"
                        echo "Harga     			: Rp.${harga[$a]}"
                        echo "Jumlah     			: ${jumlah[$a]}"
                        echo "Total      			: Rp.${total[$a]}"
                        echo "   "
                        echo "-------------------------------------------"
            else
                        echo "Data pembelian anda tidak ada,coba lagi :)"
            fi
} 
internet(){
	    firefox
}

while [ $menu != 7 ]
do
            echo "==================================================="
            echo "                  ~ APOTEK TAZEM ~ "
            echo "             Jalan menuju kebaikan No.13"
            echo "==================================================="  
            echo "1.Beli?"
            echo "2.Lihat apa yang dibeli?"
            echo "3.Bayar?"
            echo "4.Ubah apa yang dibeli?"   
            echo "5.Tidak jadi beli?"
            echo "6.Cetak pembelian?"
            echo "7.Gatau obat ? dibuka dulu dong internetnya?"
	    echo "8.Sudah selesai semua ,anda bisa keluar program"
            echo -n " yuk pilih menu ? "
            read menu
            if [ $menu -eq 1 ]
            then
                        input  
            elif [ $menu -eq 2 ]
            then
                        if [ $z -lt 1 ]
                        then
                                    echo "anda belum membeli, coba lagi :)"
                        else
                                    view
                        fi
            elif [ $menu -eq 3 ]
            then
                        pembayaran
            elif [ $menu -eq 4 ]
            then
                        update
            elif [ $menu -eq 5 ]
            then
                        delete
	    elif [ $menu -eq 6 ]
            then
                        cetak
            elif [ $menu -eq 7 ]
            then
			internet
	    elif [ $menu -eq 8 ]
            then
            echo "    Terima kasih telah mengunjungi apotek kami"  
            echo "==================================================="         
            else
                        echo "salah tulis yaa ,coba lagi :) "
            fi
            echo "	 "
done

