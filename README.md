# Matrice-Magique-en-C-
Un programme qui vérifie si une matrice est magique ou pas en langage C++.
Programme:

#include <iostream>
using namespace std;

void remplirMatrice(int mat[100][100], int n, int m);
void displayMatrice(int mat[100][100], int n, int m);
bool verifieCaracteristiques(int n, int m);
int getSumLine(int mat[100][100], int m, int indexLigne);
int getSumColone(int mat[100][100], int n,int indexCol);
int getSumDiagonale(int mat[100][100], int n);
void sumLineColDiag(int tab[100], int &k); // dans un tableau temporaire pour comparer au besoin
void displayArray(int tab[100], int k);
bool egaliteLineColDiag(int tab[100], int n);

//DECLARATIONS
    int mat[100][100],n,m,tab[100],k=0;
int main()
{
    cout<<"Donnez les dimensions de la matrice :"<<endl;
    cin>>n>>m;
    remplirMatrice(mat,n,m);
    displayMatrice(mat,n,m);
    if(verifieCaracteristiques(n,m))
    {
        // ceci est un tableau intermediaire pour contenir les sommes
        //telles que la somme de lignes, colones et diagonale pour comparer facilement
        sumLineColDiag(tab,k);
        cout<<endl<<"La tableau des sommes est: "<<endl;
        displayArray(tab,k);
        //Verification de l'egalite des sommes
        if(egaliteLineColDiag(tab,k))
            cout<<"La matrice est magique !"<<endl;
        else
            cout<<"La matrice n'est pas magique car les sommes sont differentes !"<<endl;
    }
    else
        cout<<"La matrice n'est pas magique !!!"<<endl;
    return 0;
}

//FONCTIONS
int getSumLine(int mat[100][100], int m, int indexLigne)
{
    int sum=0;
    for(int i=0; i<m; i++)
        sum+=mat[indexLigne][i];
    return sum;
}
int getSumColone(int mat[100][100], int n,int indexCol)
{
    int sum=0;
    for(int i=0; i<n; i++)
        sum+=mat[i][indexCol];
    return sum;
}
int getSumDiagonale(int mat[100][100], int n)
{
    int sum=0;
    for(int i=0; i<n; i++)
        sum+=mat[i][i];
    return sum;
}
bool verifieCaracteristiques(int n, int m)
{
    if(n==m && n%2!=0)
        return true;
    else
    {
        if(n%2 == 0)
            cout<<"la dimension de la matrice est paire !"<<endl;
        if(n != m)
            cout<<"la matrice n'est pas carree !"<<endl;
        return false;
    }
}
void remplirMatrice(int mat[100][100], int n, int m)
{
    for(int i=0; i<n; i++)
    {
        for(int j=0; j<m; j++)
        {
            cout<<"Entrer une valeur de la matrice"<<endl;
            cin>>mat[i][j];
        }
    }
}
void displayMatrice(int mat[100][100], int n, int m)
{
    for(int i=0; i<n; i++)
    {
        for(int j=0; j<m; j++)
        {
            cout<<mat[i][j]<<"\t";
        }
        cout<<endl;
    }
}

void sumLineColDiag(int tab[100], int &k)
{

    for(int j=0; j<n; j++) // somme des lignes
    {
        tab[k]=getSumLine(mat,n,j);
        k++;
    }

    for(int j=0; j<m; j++) // somme des colones
    {
        tab[k]=getSumColone(mat,m,j);
        k++;
    }
    tab[k]=getSumDiagonale(mat,n); // somme de diagonale
}
void displayArray(int tab[100], int k)
{
    for(int j=0; j<=k; j++)
    {
        cout<<tab[j]<<"\t";
    }
}
bool egaliteLineColDiag(int tab[100], int n)
{

    int tmp=0;
    for(int i=0; i<k; i++)
    {
        for(int j=i+1; j<k; j++)
        {
            if(tab[i]!=tab[j])
            {
                tmp++;
            }
        }
    }
    if(tmp==0)
        return true;
    else
        return false;
}
