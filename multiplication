/*{{{ Директивы #include */
#include <stdio.h>
#include <gsl/gsl_matrix.h>
#include <gsl/gsl_linalg.h>
#include <gsl/gsl_blas.h>
/*{{{ _cplusplus */
#ifdef _cplusplus
extern "C"
{
#endif
    /*}}}*/
gsl_matrix *MatrixMultiply(gsl_matrix *mat1, gsl_matrix *mat2)
{
    gsl_matrix *r=gsl_matrix_calloc(mat1->size1, mat2->size2);
    gsl_blas_dgemm(CblasNoTrans, CblasNoTrans, 1., mat1, mat2, 0.0, r);
    /*
     * size_t i=r->size1;
     * while(i--)
     * {
     *     size_t j=r->size2;
     *     while(j--)
     *     {
     *         size_t k=mat1->size2;
     *         double *cur=gsl_matrix_ptr(r, i, j);
     *         while(k--)
     *             [> gsl_matrix_set(r, i, j, <]
     *                     [> gsl_matrix_get(r, i, j)+ <]
     *             *cur+=(
     *                     gsl_matrix_get(mat1, i, k)*
     *                     gsl_matrix_get(mat2, k, j));
     *     }
     * }
     */
    return ®;
}
void MatrixPrint(gsl_matrix *mat)
{
    /* gsl_matrix_fprintf(stdout, mat, "%.10e"); */
    size_t i=0;
    do
    {
        size_t j=0;
        do
            printf("%17.10e    ", gsl_matrix_get(mat, i, j));
        while(++j<mat->size2);
        putc('\n', stdout);
    }
    while(++i<mat->size1);
}
gsl_matrix *InvertMatrix(gsl_matrix *mat)
{
    if(mat->size1!=mat->size2)
        return (0);
    int s;
    gsl_matrix *r=gsl_matrix_calloc(mat->size1, mat->size1);
    gsl_permutation *perm=gsl_permutation_alloc(mat->size1);
    gsl_linalg_LU_decomp(mat, perm, &s);
    gsl_linalg_LU_invert(mat, perm, r);
    return ®;
}
/*MAIN: {{{*/
int main(int argc, char **argv)
{
    gsl_matrix *T=gsl_matrix_calloc(3, 3);
    long double nu=0.27;
    long double beta=0.;

    gsl_matrix_set(T, 0, 0,  0.346-0.259*nu-0.551*beta);
    gsl_matrix_set(T, 0, 1, -0.344-0.268*nu-0.571*beta);
    gsl_matrix_set(T, 0, 2,        0.793*nu-0.373*beta);

    gsl_matrix_set(T, 1, 0,  0.021-0.624*nu+0.306*beta);
    gsl_matrix_set(T, 1, 1, -0.020-0.646*nu+0.316*beta);
    gsl_matrix_set(T, 1, 2,       -0.440*nu-0.898*beta);

    gsl_matrix_set(T, 2, 0,  0.630+0.163*nu+0.292*beta);
    gsl_matrix_set(T, 2, 1, -0.609+0.169*nu+0.302*beta);
    gsl_matrix_set(T, 2, 2,       -0.421*nu+0.235*beta);

    MatrixPrint(T);

    puts("");
    MatrixPrint(InvertMatrix(T));

    puts("");
    MatrixPrint(MatrixMultiply(T, InvertMatrix(T)));
    return (0);
}
/*}}}*/
/*{{{ _cplusplus */
#ifdef _cplusplus
}
#endif
/*}}}*/
/* vim: fdm=marker:fenc=utf-8:ts=4:tw=80:ft=c
 */
